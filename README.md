# Beyond Compare Skill

![Language](https://img.shields.io/badge/language-JavaScript-yellow.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)

> 为 Claude Code 生成 Beyond Compare 风格的代码对比 HTML 视图。专业代码审查工具，支持侧边对比、语法高亮、统计信息。

[English Version](README_EN.md)

## ✨ 核心特性

- 🔄 **侧边对比视图** - 类似 Beyond Compare/VS Code Diff 的左右并排对比
- 🎨 **VS Code Dark+ 主题** - 专业暗色主题，代码语法高亮，护眼舒适
- 📊 **统计卡片** - 显示修改文件数、行数变化、性能影响等关键指标
- 📁 **多文件切换** - 支持多个文件的对比，一键切换，清晰展示
- ⚡ **零依赖** - 完全独立的 HTML 文件，无需外部资源库
- 💻 **响应式设计** - 适配所有屏幕尺寸（桌面、平板、手机）
- 🔀 **同步滚动** - 左右代码区域自动同步滚动
- 📄 **可打印** - 支持浏览器打印功能，生成 PDF

## 🚀 快速开始

### 安装

1. **获取 Skill**
   ```bash
   # Skill 已集成在 Claude Code 中
   # 在 Claude Code 会话中直接使用
   ```

2. **触发方式**
   ```bash
   # 方式 1：直接调用
   /beyond-compare

   # 方式 2：对话中提及
   "请生成代码对比视图"

   # 方式 3：具体场景
   "按 Beyond Compare 方式展示性能优化修改"
   ```

### 基本使用

#### 场景 1：审查性能优化

```bash
用户: 完成了性能优化，请生成对比视图
Claude: [自动生成 performance-optimization-diff.html]
```

生成的文件包含：
- ✅ 所有修改文件的对比
- ✅ 性能提升统计
- ✅ 代码行数变化
- ✅ 优化说明和影响分析

#### 场景 2：审查功能添加

```bash
用户: 添加了用户认证功能，展示修改
Claude: [自动生成 user-authentication-diff.html]
```

包含内容：
- ✅ 新增文件标记（绿色）
- ✅ 修改文件的详细对比
- ✅ 删除文件标记（红色）
- ✅ 功能说明和架构影响

#### 场景 3：审查 Bug 修复

```bash
用户: 修复了 CORS 错误，对比一下
Claude: [自动生成 cors-bug-fix-diff.html]
```

包含内容：
- ✅ 修复前后代码对比
- ✅ Bug 说明和根因分析
- ✅ 修复方案详解
- ✅ 测试验证结果

## ⚙️ 配置

### 文件命名规范

生成的 HTML 文件会保存到项目根目录，文件名格式：

```
{功能描述}-diff.html
```

示例：
- `performance-optimization-diff.html` - 性能优化
- `user-authentication-diff.html` - 用户认证
- `cors-bug-fix-diff.html` - CORS Bug 修复
- `go-embed-compilation-diff.html` - Go 编译差异

### 输出说明

生成成功后，Claude 会输出：

```
✅ 代码对比视图已生成：performance-optimization-diff.html

📊 统计信息：
- Modified Files: 4
- Total Changes: +26 -25 lines
- Net Change: +1 line

🌐 使用方式：
在浏览器中打开该文件即可查看详细的代码对比。

文件包含以下功能：
- ✅ 侧边对比视图
- ✅ 语法高亮
- ✅ 文件切换
- ✅ 统计信息
```

## 📚 详细文档

### 配色方案

使用 VS Code Dark+ 主题，颜色精心选择：

| 元素 | 颜色 | 说明 |
|-----|------|------|
| 主背景 | `#1e1e1e` | 编辑器背景，极深灰 |
| 侧边栏 | `#252526` | 文件选择器，深灰 |
| 卡片背景 | `#2d2d30` | 统计卡片，稍浅灰 |
| 主文本 | `#d4d4d4` | 正常文本，浅灰 |
| 删除行 | `rgba(255, 0, 0, 0.2)` | 删除背景，红色半透明 |
| 添加行 | `rgba(0, 200, 100, 0.2)` | 添加背景，绿色半透明 |
| 关键字 | `#569cd6` | 蓝色（if, const, return） |
| 字符串 | `#ce9178` | 橙色 |
| 注释 | `#6a9955` | 绿色 |
| 函数 | `#dcdcaa` | 黄色 |

### 支持的语言

语法高亮支持以下编程语言：

- ✅ JavaScript / TypeScript
- ✅ JSON
- ✅ HTML / CSS
- ✅ Go / Rust
- ✅ Python / Shell
- ✅ Markdown
- ✅ 其他主流语言

### HTML 视图布局

```
┌─────────────────────────────────────────────────┐
│  📊 Beyond Compare Code Comparison              │
├─────────────────────────────────────────────────┤
│  📈 统计卡片区                                   │
│  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐          │
│  │Files │ │Lines │ │Added │ │Deleted│         │
│  │  4   │ │ +26  │ │ +26  │ │  -25  │         │
│  │      │ │ -25  │ │ Lines│ │ Lines │         │
│  └──────┘ └──────┘ └──────┘ └──────┘          │
├─────────────────────────────────────────────────┤
│  📁 左侧导航                 │  🔄 右侧代码对比     │
│  ▶ src/app.js              │  Before (-)  After(+)|
│  ▶ src/utils.js            │  ────────────────── │
│  ▶ config.json             │  42 - old code      │
├─────────────────────────────┤  43 + new code      │
│  点击切换查看不同文件        │  44   unchanged     │
│                             │                     │
│                             │  45 - removed line  │
│                             │  45 + added line    │
└─────────────────────────────┴─────────────────────┘
```

## 🛠️ 开发

### 本地开发环境

```bash
# 克隆项目
git clone https://github.com/mason0510/beyond-compare.git
cd beyond-compare

# 查看项目结构
tree -L 2
# beyond-compare/
# ├── README.md
# ├── README_EN.md
# ├── ARCHITECTURE.md
# ├── USAGE_AND_MAINTENANCE.md
# ├── CONTRIBUTING.md
# ├── CHANGELOG.md
# ├── TODOS.md
# ├── LICENSE
# ├── .gitignore
# ├── SKILL.md (Claude Code Skill 定义)
# └── src/
#     └── beyond-compare.js

# 本地测试
# 1. 在 Claude Code 中加载此 skill
# 2. 运行 /beyond-compare 测试生成

# 代码检查
npm run lint

# 运行测试
npm test
```

### 项目结构说明

```
beyond-compare/
├── README.md                  # 中文项目说明
├── README_EN.md              # 英文项目说明
├── ARCHITECTURE.md           # 架构设计文档
├── USAGE_AND_MAINTENANCE.md  # 使用和维护指南
├── CONTRIBUTING.md           # 贡献指南
├── CHANGELOG.md              # 变更日志
├── TODOS.md                  # 待办和已知问题
├── LICENSE                   # MIT 许可证
├── .gitignore               # Git 忽略规则
├── SKILL.md                 # Claude Code Skill 定义（核心）
└── src/
    ├── beyond-compare.js    # 主要实现逻辑
    └── template/           # HTML 模板
        └── diff-template.html
```

### 修改和扩展

#### 添加新的配色方案

在 `src/beyond-compare.js` 中找到配色变量部分：

```javascript
const colors = {
    primary: '#1e1e1e',
    secondary: '#252526',
    // ... 其他颜色
};
```

修改后重新生成即可。

#### 添加新的语言支持

在语法高亮部分添加正则表达式规则：

```javascript
const highlightPatterns = {
    'new-language': [
        { pattern: /pattern1/, class: 'kw' },
        { pattern: /pattern2/, class: 'str' },
    ]
};
```

## 📧 联系方式

- **GitHub**: [@mason0510](https://github.com/mason0510)
- **Email**: zhang_989898@126.com
- **WeChat**: zhcmason
- **Issues**: [GitHub Issues](https://github.com/mason0510/beyond-compare/issues)

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE)

本项目采用 MIT 许可证。你可以自由地使用、修改和分发此项目，但需要保留原始版权声明和许可证文本。

## 🤝 贡献

欢迎贡献！无论是报告问题、提出建议还是提交代码，都对我们很有帮助。

请参考 [CONTRIBUTING.md](CONTRIBUTING.md) 了解详细的贡献指南。

## 更新日志

### v1.0.0 (2026-03-14)
- ✨ 初始版本发布
- ✨ 支持侧边对比视图
- ✨ VS Code Dark+ 主题
- ✨ 多文件切换功能
- ✨ 完整的统计信息显示
- ✨ 同步滚动支持

详见 [CHANGELOG.md](CHANGELOG.md) 获取完整的版本历史。

---

**最后更新**: 2026-03-14
**维护者**: Mason ([@mason0510](https://github.com/mason0510))
