# Changelog

所有显著的项目更改都记录在此文件中。

该项目遵循 [Semantic Versioning](https://semver.org/)。

## [Unreleased]

### Added
- (待发布功能)

### Changed
- (待发布变更)

### Fixed
- (待发布修复)

---

## [1.0.0] - 2026-03-14

### Added
- ✨ 首个稳定版本发布
- ✨ 侧边对比视图（左右并排对比）
- ✨ VS Code Dark+ 配色主题
- ✨ 多文件切换功能
- ✨ 统计卡片（文件数、行数变化）
- ✨ 同步滚动支持
- ✨ 基础语法高亮（JS/HTML/JSON/CSS/Shell）
- ✨ 零依赖（完全独立的 HTML）
- ✨ 响应式设计
- ✨ 可打印/导出为 PDF

### Documentation
- 📄 完整中英文 README
- 📄 架构设计文档（ARCHITECTURE.md）
- 📄 使用和维护指南（USAGE_AND_MAINTENANCE.md）
- 📄 贡献指南（CONTRIBUTING.md）
- 📄 待办事项清单（TODOS.md）
- 📄 MIT 许可证

---

## 版本发布计划

### v1.1.0 - 计划于 2026-04-15

**高优先级修复**
- 🔧 修复移动设备响应式问题，添加单栏模式
- 🚀 实现虚拟滚动，支持 500+ 行大文件
- 🛡️ 增强敏感信息检测（API Key、密码过滤）
- ✅ 完整浏览器兼容性测试（Chrome、Firefox、Safari、Edge）

### v1.2.0 - 计划于 2026-05-15

**功能扩展**
- 🔍 添加搜索功能（关键词搜索、正则表达式）
- 🎯 添加过滤选项（新增/删除/修改行过滤）
- 🌐 扩展语言支持（Go、Rust、Ruby、PHP）
- 📊 性能分析集成

### v1.3.0 - 计划于 2026-06-15

**高级功能**
- 📥 导出功能（PDF、Markdown、纯文本）
- 🎨 深色/浅色主题切换
- 🌍 国际化支持（i18n）
- 👥 团队协作注释功能

---

## 历史变更详解

### 初始开发阶段

项目始于 2026-01-29，旨在为 Claude Code 提供专业的代码对比视图工具。

**设计理念**：
- 零依赖：避免外部库依赖，确保最大兼容性
- 离线优先：完全独立的 HTML 文件，支持离线使用
- 用户友好：直观的交互，无学习曲线

**技术选型**：
- 纯 HTML/CSS/JavaScript（Vanilla JS）
- VS Code Dark+ 主题（专业配色）
- 正则表达式语法高亮（轻量级）

### v1.0.0 发布（2026-03-14）

**核心功能**完成，达到生产就绪状态。

关键里程碑：
- ✅ 侧边对比视图工作正常
- ✅ 支持多种编程语言
- ✅ 统计信息准确
- ✅ 浏览器兼容性良好（Chrome 90+、Firefox 88+）
- ✅ 文档完整

已知限制（后续版本改进）：
- 移动设备体验一般（计划 v1.1.0 改进）
- 大文件加载有点慢（计划 v1.1.0 虚拟滚动）
- 语言支持不够全面（计划 v1.2.0 扩展）

---

## 贡献者

感谢以下贡献者的支持（将在首个稳定版后更新）：

- Mason ([@mason0510](https://github.com/mason0510)) - 项目维护者

---

## 许可证

MIT License - 详见 [LICENSE](LICENSE)

---

## 参考资源

- [Semantic Versioning](https://semver.org/)
- [Keep a Changelog](https://keepachangelog.com/)
- [Conventional Commits](https://www.conventionalcommits.org/)

---

**最后更新**: 2026-03-14
**维护者**: Mason
