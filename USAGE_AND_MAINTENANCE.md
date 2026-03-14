# 使用和维护指南

## 第一部分：使用指南

### 安装

#### 前置要求
- Claude Code CLI 工具已安装
- 浏览器支持：Chrome 90+、Firefox 88+、Safari 14+
- 操作系统：macOS、Linux 或 Windows

#### 安装步骤

Beyond Compare Skill 已内置于 Claude Code，无需额外安装。

1. **启动 Claude Code**
   ```bash
   claude
   ```

2. **在会话中调用**
   ```bash
   /beyond-compare
   ```

### 基础使用

#### 命令说明

| 命令 | 说明 | 输出 |
|------|------|------|
| `/beyond-compare` | 生成代码对比 | `{功能描述}-diff.html` |
| 对话提及 "对比" | 自动触发 | 同上 |

#### 常见场景

**场景 1：初次使用**
1. 修改代码并在 Claude Code 中提交
2. 对话中说："生成对比视图"
3. Claude 会自动识别修改并生成 HTML
4. 在浏览器中打开生成的文件

**场景 2：高级用法 - 性能优化展示**
1. 完成性能优化修改
2. 对话：`performance-optimization-diff.html`
3. Claude 生成带有性能指标的对比视图

### 配置和自定义

#### 输出文件位置

生成的 HTML 文件默认保存到项目根目录。文件名根据功能自动生成：

```
性能优化       → performance-optimization-diff.html
功能添加       → feature-addition-diff.html
Bug 修复       → bug-fix-diff.html
代码重构       → refactoring-diff.html
```

#### 自定义配色方案

编辑生成的 HTML 文件，修改 CSS 变量：

```html
<style>
  :root {
    --bg-primary: #1e1e1e;        /* 修改主背景色 */
    --added-bg: rgba(0,200,100,0.18);  /* 修改新增行背景 */
    --removed-bg: rgba(255,80,80,0.18); /* 修改删除行背景 */
  }
</style>
```

#### 常见配置示例

**示例 1：浅色主题**
```css
:root {
  --bg-primary: #ffffff;
  --text-primary: #333333;
  --added-bg: rgba(0, 255, 0, 0.1);
  --removed-bg: rgba(255, 0, 0, 0.1);
}
```

**示例 2：高对比度（可访问性）**
```css
:root {
  --bg-primary: #000000;
  --text-primary: #ffffff;
  --added-text: #00ff00;
  --removed-text: #ff0000;
}
```

**示例 3：打印友好**
```css
@media print {
  .file-nav { display: none; }
  .diff-column { flex: 1; }
}
```

---

## 第二部分：维护指南

### 代码结构

```
src/
├── beyond-compare.js    # 主要实现（≈ 400 行）
│   ├── dataExtraction() # 数据提取
│   ├── generateHTML()   # HTML 生成
│   └── setupInteraction() # 交互设置
│
└── template/
    └── diff-template.html  # HTML 基础模板
```

### 本地开发环境设置

```bash
# 克隆仓库
git clone https://github.com/kcd-dev/tcd-beyond-compare.git
cd tcd-beyond-compare

# 安装依赖（如果有）
npm install

# 运行开发服务器（可选）
npm run dev

# 运行测试
npm test

# 构建（可选）
npm run build
```

### 常见维护任务

#### 1. 添加新特性的步骤

1. **创建特性分支**
   ```bash
   git checkout -b feature/new-feature
   ```

2. **编写代码**
   - 在 `src/beyond-compare.js` 中实现
   - 保持代码简洁，不超过 50 行/函数

3. **添加测试**
   - 编写单元测试验证功能
   - 测试覆盖率目标：80%+

4. **更新文档**
   - 更新 README.md（新功能说明）
   - 更新 ARCHITECTURE.md（如涉及架构变更）
   - 更新 USAGE_AND_MAINTENANCE.md（使用说明）

5. **提交 PR**
   ```bash
   git add .
   git commit -m "feat: add new feature description"
   git push origin feature/new-feature
   ```

#### 2. 修复 Bug 的流程

1. **定位问题**
   - 查看错误日志和用户反馈
   - 尝试复现问题
   - 确认影响范围

2. **编写测试复现 Bug**
   ```javascript
   test('should handle empty files', () => {
     const result = generateHTML({ files: [] });
     expect(result).toBeTruthy();
   });
   ```

3. **修复代码**
   - 修改相关代码
   - 确保测试通过

4. **验证修复**
   ```bash
   npm test          # 验证所有测试通过
   npm run lint      # 代码风格检查
   ```

5. **更新 CHANGELOG**
   ```markdown
   ### [Bugfix] Fixed issue #123
   - Fixed empty files handling
   - Added regression test
   ```

#### 3. 发布新版本

1. **更新版本号**
   ```bash
   # 在 package.json 中修改版本号
   # v1.0.0 → v1.0.1 (patch)
   # v1.0.0 → v1.1.0 (minor)
   # v1.0.0 → v2.0.0 (major)
   ```

2. **更新 CHANGELOG**
   ```markdown
   ## [1.0.1] - 2026-03-20
   ### Fixed
   - Fixed empty files handling
   ### Changed
   - Improved syntax highlighting
   ```

3. **运行完整测试**
   ```bash
   npm test -- --coverage
   ```

4. **创建 Git Tag**
   ```bash
   git tag -a v1.0.1 -m "Release version 1.0.1"
   git push origin v1.0.1
   ```

5. **发布发布说明**
   - 在 GitHub Releases 中创建发布
   - 包含 CHANGELOG 内容
   - 附加相关文件（如适用）

### 调试和故障排查

#### 常见问题及解决方案

**问题 1：生成的 HTML 文件无法打开**
- 现象：浏览器显示 404 或空白页
- 原因：文件路径不正确或文件未生成
- 解决方案：
  ```bash
  # 检查文件是否存在
  ls -la *.html
  # 检查文件权限
  chmod 644 {filename}.html
  # 用绝对路径打开
  open $(pwd)/{filename}.html
  ```

**问题 2：代码对比显示不完整**
- 现象：某些修改行未显示
- 原因：数据提取逻辑有误
- 解决方案：
  - 检查数据提取函数的正则表达式
  - 增加测试用例覆盖边界情况
  - 查看浏览器控制台错误信息

**问题 3：页面加载缓慢**
- 现象：大文件对比响应慢
- 原因：JavaScript 渲染效率低
- 解决方案：
  - 对大于 500 行的文件启用虚拟滚动
  - 使用 Web Worker 异步处理数据
  - 考虑分页显示

#### 性能优化

已知的性能瓶颈和优化建议：

| 瓶颈 | 原因 | 优化方案 |
|-----|------|--------|
| 大文件加载慢 | 一次性 DOM 渲染 | 虚拟滚动、分页 |
| 语法高亮耗时 | 正则表达式运算 | Web Worker 异步 |
| 文件切换延迟 | 重绘整个页面 | 只切换展示，保留 DOM |
| 内存占用高 | 保留所有代码在 DOM | 延迟渲染只显示区域 |

#### 代码质量维护

运行代码检查工具：

```bash
# 代码风格检查
npm run lint

# 格式化代码
npm run format

# 运行完整测试
npm test -- --coverage

# 代码复杂度分析
npm run complexity
```

### 依赖管理

#### 如何更新依赖

当前 Beyond Compare 零依赖，无需更新依赖。

如果未来需要添加依赖（不推荐）：

```bash
# 查看过时的依赖
npm outdated

# 更新单个依赖
npm install package-name@latest

# 更新所有依赖
npm update
```

#### 依赖安全检查

```bash
# 审计已知安全漏洞
npm audit

# 修复安全漏洞
npm audit fix

# 仅显示高风险漏洞
npm audit --severity=high
```

#### 添加新依赖的检查清单

- [ ] 依赖的大小合理吗？（<100KB）
- [ ] 依赖是否活跃维护？（最近 6 个月有更新）
- [ ] 是否有安全问题？（运行 npm audit）
- [ ] 许可证是否兼容？（MIT/Apache/BSD）
- [ ] 是否有现成替代方案？

**建议**：尽可能保持零依赖，使用原生 JavaScript API。

### 文档维护

- ✅ 保持 README 与代码同步
- ✅ 更新 API 文档
- ✅ 添加新功能的使用示例
- ✅ 维护更新日志（CHANGELOG）

### 监控和日志

#### 如何添加日志

```javascript
// 在关键位置添加 console.log
if (DEBUG_MODE) {
  console.log('[Beyond Compare] Extracted files:', files);
  console.log('[Beyond Compare] Generated HTML size:', htmlSize);
}
```

#### 常见日志位置

- 浏览器控制台：`F12` → Console
- 生成输出：检查 Claude Code 输出信息

### 发布前检查清单

发布新版本前必须完成：

- [ ] 所有测试通过（100% 通过率）
- [ ] 代码风格检查通过
- [ ] 文档已更新
- [ ] README（中英文）已同步
- [ ] CHANGELOG 已更新
- [ ] 版本号正确更新
- [ ] 没有硬编码的敏感信息
- [ ] 依赖已审查

### 长期维护建议

1. **定期更新**
   - 每季度检查一次浏览器兼容性
   - 每半年审查一次代码架构

2. **社区反馈**
   - 及时回复 Issue（24 小时内）
   - 定期审查和合并 PR

3. **性能监控**
   - 持续关注生成时间
   - 定期性能基准测试

4. **代码审查**
   - 所有代码 PR 都应该审查
   - 保持代码质量和一致性

5. **交接准备**
   - 维护清晰的文档
   - 记录关键决策和架构
   - 为新维护者编写指南

---

**文档最后更新**: 2026-03-14
