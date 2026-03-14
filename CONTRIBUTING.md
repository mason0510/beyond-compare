# 贡献指南

感谢你对 Beyond Compare 项目的关注！我们欢迎所有形式的贡献。

## 🙏 贡献方式

### 报告 Bug

如果你发现了问题，请：

1. **使用 GitHub Issues**
   - 点击 [New Issue](https://github.com/kcd-dev/tcd-beyond-compare/issues/new)
   - 选择 "Bug Report" 模板

2. **清晰描述问题**
   - 标题：简短说明问题（如："移动端显示错乱"）
   - 描述：详细的问题说明
   - 环境：操作系统、浏览器版本
   - 复现步骤：具体的重现方式

3. **包含相关信息**
   - 错误信息或截图
   - 影响的文件或场景
   - 期望的行为与实际行为的对比

**示例**：
```
标题：大文件对比时首屏加载缓慢

环境：
- 操作系统：macOS 12
- 浏览器：Chrome 120
- 文件大小：>1000 行代码

复现步骤：
1. 生成包含 1000+ 行代码的对比
2. 打开 HTML 文件
3. 观察加载时间和滚动流畅度

期望行为：首屏加载 <500ms

实际行为：加载需要 2-3 秒，滚动卡顿
```

### 提交特性请求

有新功能建议？

1. **使用 GitHub Issues**
   - 点击 [New Issue](https://github.com/kcd-dev/tcd-beyond-compare/issues/new)
   - 选择 "Feature Request" 模板

2. **说明需求背景**
   - 为什么需要这个功能？
   - 解决什么问题？

3. **描述期望的行为**
   - 功能应该做什么？
   - 使用场景是什么？

**示例**：
```
标题：添加搜索功能

需求背景：
对比大文件时，需要快速定位特定的修改

期望功能：
- 支持在代码中搜索关键词
- 高亮显示匹配的行
- 支持 Ctrl+F 快捷键

使用场景：
- 在 500+ 行的对比中快速找到特定函数的修改
```

### 提交代码

想要为项目做贡献？遵循以下流程：

#### 1. Fork 和 Clone

```bash
# Fork 项目到你的账户
# 然后 Clone 你的 Fork
git clone https://github.com/YOUR-USERNAME/tcd-beyond-compare.git
cd tcd-beyond-compare
```

#### 2. 创建特性分支

```bash
# 创建描述性的分支名
git checkout -b feature/add-search-functionality
# 或修复分支
git checkout -b fix/mobile-responsive-issue
# 或文档分支
git checkout -b docs/update-usage-guide
```

#### 3. 编写代码

遵循项目的代码规范：
- 代码清晰易读
- 单个函数不超过 50 行
- 添加必要的注释说明复杂逻辑

#### 4. 编写测试

为你的修改添加测试用例：

```bash
npm test
```

目标：新增代码的测试覆盖率 ≥ 80%

#### 5. 更新文档

修改涉及的文档：
- `README.md` - 如有新功能
- `ARCHITECTURE.md` - 如有架构变更
- `USAGE_AND_MAINTENANCE.md` - 如有使用变更
- `CHANGELOG.md` - 在 [Unreleased] 下添加条目

#### 6. 提交更改

```bash
git add .
git commit -m "feat: add search functionality in code diff view"
```

遵循 Conventional Commits 格式（见下面）

#### 7. 推送到你的 Fork

```bash
git push origin feature/add-search-functionality
```

#### 8. 打开 Pull Request

1. 访问原项目 GitHub 页面
2. 点击 "Create Pull Request"
3. 选择你的分支
4. 填写 PR 信息：
   - 标题清晰准确
   - 说明修改内容
   - 引用相关的 Issue（如 `Closes #123`）
   - 附加截图或演示链接

---

## 提交信息规范

使用 Conventional Commits 格式：

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type 类型

| Type | 说明 | 示例 |
|------|------|------|
| `feat` | 新功能 | `feat: add search in diff view` |
| `fix` | Bug 修复 | `fix: mobile responsive layout` |
| `docs` | 文档更新 | `docs: update README` |
| `style` | 格式调整 | `style: reformat code blocks` |
| `refactor` | 代码重构 | `refactor: simplify HTML generation` |
| `perf` | 性能优化 | `perf: implement virtual scroll` |
| `test` | 测试相关 | `test: add unit tests for data extraction` |
| `chore` | 工具配置 | `chore: update dependencies` |

### 示例提交

```bash
# 简单的 Bug 修复
git commit -m "fix: correct mobile layout overflow issue"

# 新功能带详细说明
git commit -m "feat: add search functionality to diff view

- Implement search box in header
- Highlight matching lines
- Support regex patterns
- Add keyboard shortcut (Ctrl+F)

Closes #42"

# 文档更新
git commit -m "docs: add search feature to USAGE_AND_MAINTENANCE.md"
```

---

## 行为准则

本项目遵循开源社区规范。参与者应该：

### ✅ 应该做的

- 尊重他人的观点和经验
- 使用包容和建设性的语言
- 专注于对项目的帮助
- 接受建设性批评
- 主动报告滥用行为给项目维护者

### ❌ 禁止的行为

- 骚扰、歧视、仇恨言论
- 无谓的人身攻击或辱骂
- 垃圾信息和无关广告
- 商业推广
- 违反开源许可证的行为

任何违反行为准则的行为将被记录，严重情况下将被禁止参与项目。

---

## 开发规范

### 代码风格

- 遵循现有代码风格
- 使用 2 空格缩进
- 最大行长 100 字符
- 运行代码检查：`npm run lint`

### 测试

- 为新功能编写测试
- 为 Bug 修复添加回归测试
- 确保所有测试通过：`npm test`
- 目标覆盖率：≥ 80%

### 性能

- 避免性能退化
- 大文件（>500 行）测试加载时间
- 内存占用合理

### 安全

- 禁止硬编码敏感信息
- 验证用户输入
- 不包含已知安全漏洞的依赖

---

## 审查流程

### 我们会关注

✅ **好的 PR**：
- 清晰的提交信息
- 充分的测试覆盖
- 文档已更新
- 代码风格一致
- 性能无退化

❌ **可能被拒绝的 PR**：
- 缺少测试
- 文档不完整
- 代码风格不一致
- 包含硬编码密钥
- 重大性能问题

### 审查时间

- 简单修复（<100 行代码）：1-2 天
- 普通功能：2-5 天
- 重大变更：5-10 天

---

## 联系和获取帮助

- **问题/讨论**：GitHub Issues
- **实时讨论**：GitHub Discussions
- **电子邮件**：zhang_989898@126.com
- **WeChat**: zhcmason

---

感谢你的贡献！🙌

**维护者**: Mason ([@mason0510](https://github.com/mason0510))
