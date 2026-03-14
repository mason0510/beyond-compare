# 项目架构说明 | Architecture

## 整体架构设计

Beyond Compare Skill 是 Claude Code 的代码对比视图生成器，架构设计遵循"**模板驱动 + 数据映射**"模式。

```
┌─────────────────────────────────────────────────────────┐
│          Claude Code 对话会话                           │
│  （用户提供代码修改内容或上下文）                       │
└────────────────────┬────────────────────────────────────┘
                     │ 解析修改内容
                     ▼
┌─────────────────────────────────────────────────────────┐
│     数据提取层 (Data Extraction)                        │
│  ├─ 识别修改文件列表                                   │
│  ├─ 提取修改前后代码片段                               │
│  ├─ 计算统计信息（行数、文件数）                       │
│  └─ 标记修改类型（新增、删除、修改）                   │
└────────────────────┬────────────────────────────────────┘
                     │ 结构化数据
                     ▼
┌─────────────────────────────────────────────────────────┐
│     HTML 生成层 (HTML Generation)                      │
│  ├─ 加载 HTML 模板                                     │
│  ├─ 注入统计数据 (stats)                               │
│  ├─ 编译文件列表 (files)                               │
│  ├─ 生成对比代码块 (diffs)                             │
│  └─ 应用样式和交互脚本                                │
└────────────────────┬────────────────────────────────────┘
                     │ 完整 HTML 文档
                     ▼
┌─────────────────────────────────────────────────────────┐
│    文件输出 (File Output)                              │
│  {feature-description}-diff.html                        │
│  （保存到项目根目录）                                   │
└────────────────────┬────────────────────────────────────┘
                     │ 通知用户
                     ▼
┌─────────────────────────────────────────────────────────┐
│        用户在浏览器中打开查看                           │
│   ✅ 侧边对比 ✅ 语法高亮 ✅ 交互                      │
└─────────────────────────────────────────────────────────┘
```

## 核心模块设计

### 1. 数据提取层 (Data Extraction)

**职责**：从会话上下文中提取代码修改信息

**主要任务**：
- 识别哪些文件被修改、新增、删除
- 提取修改前后的代码片段
- 计算修改统计（行数增减、文件数等）
- 标记修改类型（added/removed/modified）

**输出数据结构**：
```javascript
{
  stats: {
    modifiedFiles: 4,
    totalLines: 51,      // +26 -25
    addedLines: 26,
    removedLines: 25,
    netChange: 1
  },
  files: [
    {
      name: "src/app.js",
      type: "modified",   // added | removed | modified
      changes: {
        lines: [
          { type: "context", lineNo: 42, content: "old code" },
          { type: "removed", lineNo: 43, content: "delete line" },
          { type: "added", lineNo: 44, content: "new line" }
        ]
      }
    },
    // ...更多文件
  ]
}
```

### 2. HTML 生成层 (HTML Generation)

**职责**：将结构化数据转换为交互式 HTML 页面

**主要任务**：
- 加载并解析 HTML 模板
- 注入数据（stats、files、diffs）
- 生成 CSS 样式（内联）
- 生成交互脚本（内联）
- 应用语法高亮规则

**关键特性**：
- **零依赖**：所有 CSS 和 JavaScript 都内联在 HTML 中
- **自包含**：单个 HTML 文件，可离线使用
- **响应式**：使用 CSS Grid 和 Flexbox 适配各种屏幕

### 3. 交互层 (Interaction)

**职责**：提供用户交互功能

**实现功能**：
- **文件切换**：点击文件名切换不同的对比视图
- **同步滚动**：左右代码区同时滚动
- **行号导航**：点击行号定位到特定位置
- **差异高亮**：自动高亮修改行

**实现方式**：
```javascript
// 文件切换
document.querySelectorAll('.file-item').forEach(item => {
  item.addEventListener('click', () => {
    // 1. 隐藏所有 diff 面板
    // 2. 显示选中文件的面板
    // 3. 更新导航样式
  });
});

// 同步滚动
let syncing = false;
leftColumn.addEventListener('scroll', () => {
  if (!syncing) {
    syncing = true;
    rightColumn.scrollTop = leftColumn.scrollTop;
    syncing = false;
  }
});
```

## 数据流向

```
用户对话
  │
  ├─ 包含代码修改信息
  │
  ▼
数据提取器
  │
  ├─ 分析修改文件列表
  ├─ 提取 before/after 代码
  ├─ 计算统计数据
  │
  ▼
数据结构 (JSON)
  │
  ├─ files: [修改文件数组]
  ├─ stats: {统计信息}
  │
  ▼
HTML 生成器
  │
  ├─ 读取模板
  ├─ 注入数据
  ├─ 生成 HTML
  │
  ▼
HTML 文件输出
  │
  ├─ 保存到磁盘
  ├─ 通知用户
  │
  ▼
用户浏览器
  │
  ├─ 加载 HTML
  ├─ 渲染页面
  ├─ 触发交互
```

## 关键设计决策

### 1. 为什么使用零依赖 HTML？

**优势**：
- ✅ 用户无需安装任何工具或库
- ✅ HTML 文件可离线使用
- ✅ 快速加载，没有网络延迟
- ✅ 安全性高，完全本地

**权衡**：
- ⚠️ 代码量略大（但仍在可接受范围）
- ⚠️ 语法高亮功能基础（使用正则表达式而非完整解析器）

### 2. 为什么使用侧边对比而非行内对比？

**优势**：
- ✅ 清晰易读，看整体代码流
- ✅ 支持长行代码，不需换行
- ✅ 符合业界标准（Beyond Compare、GitHub Diff）
- ✅ 支持同步滚动

**限制**：
- ⚠️ 屏幕宽度要求较高
- ⚠️ 移动端不够友好（已通过响应式改进）

### 3. 为什么使用 CSS 变量定制主题？

**优势**：
- ✅ 易于更换配色方案
- ✅ 减少代码重复
- ✅ 运行时动态修改（可选扩展）

```css
:root {
  --bg-primary: #1e1e1e;
  --text-primary: #d4d4d4;
  --added-bg: rgba(0, 200, 100, 0.18);
  /* ... 更多颜色 */
}
```

## 扩展和维护

### 如何添加新功能

#### 1. 添加新的统计指标

在数据提取层添加计算逻辑：

```javascript
// src/beyond-compare.js
const stats = {
  modifiedFiles: files.length,
  addedLines: countLines(type === 'added'),
  performanceImpact: calculateImpact(),  // 新增
  // ...
};
```

#### 2. 添加新的交互功能

在 HTML 脚本部分添加事件监听：

```javascript
// 新增：搜索功能
const searchBox = document.getElementById('search');
searchBox.addEventListener('input', (e) => {
  highlightSearchResults(e.target.value);
});
```

#### 3. 支持新的编程语言

在语法高亮部分添加规则：

```javascript
const languageRules = {
  'go': [
    { pattern: /\bfunc\b/, class: 'kw' },
    { pattern: /\bpackage\b/, class: 'kw' },
    // ...
  ]
};
```

### 性能考虑

**当前性能指标**：
- 文件大小：约 50-100KB（包含 CSS、JS、初始 HTML）
- 生成时间：<100ms（简单对比）、<500ms（复杂对比）
- 首屏加载：<1s（本地文件）

**优化建议**：
- 大文件（>500 行）可考虑虚拟滚动
- 多于 10 个文件时考虑延迟渲染
- 未来可考虑 Web Worker 异步处理

## 技术栈

| 层级 | 技术 | 说明 |
|-----|------|------|
| 数据 | JavaScript | 数据结构和处理逻辑 |
| 渲染 | HTML5 | 语义化标签 |
| 样式 | CSS3 | Grid、Flexbox、CSS Variables |
| 交互 | Vanilla JavaScript | 无任何库依赖 |
| 高亮 | RegExp | 正则表达式语法匹配 |

## 文件组织

```
src/
├── beyond-compare.js          # 主要逻辑
│   ├── Data Extraction        # 数据提取
│   ├── HTML Generation        # HTML 生成
│   ├── Interaction Setup      # 交互设置
│   └── Utility Functions      # 工具函数
│
└── template/
    └── diff-template.html     # HTML 基础模板
        ├── <head>            # Meta、样式
        ├── <body>            # 结构
        └── <script>          # 交互脚本
```

## 总结

Beyond Compare Skill 采用**关注点分离**（Separation of Concerns）原则：

- **数据层**：独立处理数据提取和转换
- **表现层**：专注 HTML/CSS 的生成和渲染
- **交互层**：管理用户交互和事件
- **无外部依赖**：确保最高的可用性和安全性

这样的设计确保了项目的可维护性、可扩展性和用户体验。
