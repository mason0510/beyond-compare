# Beyond Compare Skill

![Language](https://img.shields.io/badge/language-JavaScript-yellow.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)

> Generate Beyond Compare style code diff HTML views for Claude Code. Professional code review tool with side-by-side comparison, syntax highlighting, and statistics.

[中文版本](README.md)

## ✨ Core Features

- 🔄 **Side-by-Side Comparison** - Like Beyond Compare/VS Code Diff with left-right split view
- 🎨 **VS Code Dark+ Theme** - Professional dark theme with syntax highlighting for comfortable viewing
- 📊 **Statistics Cards** - Display modified files count, line changes, performance impact metrics
- 📁 **Multi-File Switch** - Support multiple file comparisons with one-click switching
- ⚡ **Zero Dependencies** - Completely standalone HTML file, no external libraries required
- 💻 **Responsive Design** - Adapts to all screen sizes (desktop, tablet, mobile)
- 🔀 **Sync Scroll** - Left and right code areas scroll synchronously
- 📄 **Printable** - Support browser printing for PDF export

## 🚀 Quick Start

### Installation

1. **Get the Skill**
   ```bash
   # Skill is integrated in Claude Code
   # Use directly in Claude Code sessions
   ```

2. **Trigger Methods**
   ```bash
   # Method 1: Direct command
   /beyond-compare

   # Method 2: In conversation
   "Generate a code comparison view"

   # Method 3: Specific scenario
   "Show the performance optimization changes in Beyond Compare style"
   ```

### Basic Usage

#### Scenario 1: Review Performance Optimization

```bash
User: I've completed performance optimization, generate the comparison view
Claude: [Automatically generates performance-optimization-diff.html]
```

Generated file includes:
- ✅ Side-by-side comparison of all modified files
- ✅ Performance improvement statistics
- ✅ Code line changes
- ✅ Optimization explanations and impact analysis

#### Scenario 2: Review Feature Addition

```bash
User: Added user authentication feature, show the changes
Claude: [Automatically generates user-authentication-diff.html]
```

Contents include:
- ✅ New files marked in green
- ✅ Detailed comparison of modified files
- ✅ Deleted files marked in red
- ✅ Feature explanation and architecture impact

#### Scenario 3: Review Bug Fix

```bash
User: Fixed CORS error, compare the changes
Claude: [Automatically generates cors-bug-fix-diff.html]
```

Contents include:
- ✅ Before and after code comparison
- ✅ Bug explanation and root cause analysis
- ✅ Fix solution details
- ✅ Test verification results

## ⚙️ Configuration

### File Naming Convention

Generated HTML files are saved to the project root directory with the format:

```
{feature-description}-diff.html
```

Examples:
- `performance-optimization-diff.html` - Performance optimization
- `user-authentication-diff.html` - User authentication
- `cors-bug-fix-diff.html` - CORS bug fix
- `go-embed-compilation-diff.html` - Go compilation comparison

### Output Format

Upon successful generation, Claude outputs:

```
✅ Code comparison view generated: performance-optimization-diff.html

📊 Statistics:
- Modified Files: 4
- Total Changes: +26 -25 lines
- Net Change: +1 line

🌐 How to use:
Open the HTML file in your browser to view the detailed code comparison.

The file includes:
- ✅ Side-by-side comparison view
- ✅ Syntax highlighting
- ✅ File switching
- ✅ Statistics information
```

## 📚 Documentation

### Color Scheme

Uses VS Code Dark+ theme with carefully selected colors:

| Element | Color | Description |
|---------|-------|-------------|
| Main Background | `#1e1e1e` | Editor background, very dark gray |
| Sidebar | `#252526` | File selector, dark gray |
| Card Background | `#2d2d30` | Statistics cards, slightly lighter gray |
| Main Text | `#d4d4d4` | Normal text, light gray |
| Deleted Line | `rgba(255, 0, 0, 0.2)` | Deleted background, semi-transparent red |
| Added Line | `rgba(0, 200, 100, 0.2)` | Added background, semi-transparent green |
| Keywords | `#569cd6` | Blue (if, const, return) |
| Strings | `#ce9178` | Orange |
| Comments | `#6a9955` | Green |
| Functions | `#dcdcaa` | Yellow |

### Supported Languages

Syntax highlighting supports the following programming languages:

- ✅ JavaScript / TypeScript
- ✅ JSON
- ✅ HTML / CSS
- ✅ Go / Rust
- ✅ Python / Shell
- ✅ Markdown
- ✅ Other mainstream languages

### HTML View Layout

```
┌─────────────────────────────────────────────────┐
│  📊 Beyond Compare Code Comparison              │
├─────────────────────────────────────────────────┤
│  📈 Statistics Cards                            │
│  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐          │
│  │Files │ │Lines │ │Added │ │Deleted│         │
│  │  4   │ │ +26  │ │ +26  │ │  -25  │         │
│  │      │ │ -25  │ │ Lines│ │ Lines │         │
│  └──────┘ └──────┘ └──────┘ └──────┘          │
├─────────────────────────────────────────────────┤
│  📁 Left Navigation      │  🔄 Right Code Diff  │
│  ▶ src/app.js           │  Before (-)  After(+) │
│  ▶ src/utils.js         │  ────────────────── │
│  ▶ config.json          │  42 - old code       │
├──────────────────────────┤  43 + new code       │
│  Click to switch files   │  44   unchanged      │
│                          │                      │
│                          │  45 - removed line   │
│                          │  45 + added line     │
└──────────────────────────┴──────────────────────┘
```

## 🛠️ Development

### Local Development Environment

```bash
# Clone the project
git clone https://github.com/mason0510/beyond-compare.git
cd beyond-compare

# View project structure
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
# ├── SKILL.md (Claude Code Skill definition)
# └── src/
#     └── beyond-compare.js

# Local testing
# 1. Load this skill in Claude Code
# 2. Run /beyond-compare to test generation

# Code checking
npm run lint

# Run tests
npm test
```

### Project Structure

```
beyond-compare/
├── README.md                  # Chinese project documentation
├── README_EN.md              # English project documentation
├── ARCHITECTURE.md           # Architecture design document
├── USAGE_AND_MAINTENANCE.md  # Usage and maintenance guide
├── CONTRIBUTING.md           # Contribution guidelines
├── CHANGELOG.md              # Change log
├── TODOS.md                  # Todos and known issues
├── LICENSE                   # MIT License
├── .gitignore               # Git ignore rules
├── SKILL.md                 # Claude Code Skill definition (core)
└── src/
    ├── beyond-compare.js    # Main implementation logic
    └── template/           # HTML templates
        └── diff-template.html
```

### Customization

#### Add New Color Scheme

Find the color variables section in `src/beyond-compare.js`:

```javascript
const colors = {
    primary: '#1e1e1e',
    secondary: '#252526',
    // ... other colors
};
```

Modify and regenerate.

#### Add Language Support

Add regex patterns in the syntax highlighting section:

```javascript
const highlightPatterns = {
    'new-language': [
        { pattern: /pattern1/, class: 'kw' },
        { pattern: /pattern2/, class: 'str' },
    ]
};
```

## 📧 Contact

- **GitHub**: [@mason0510](https://github.com/mason0510)
- **Email**: zhang_989898@126.com
- **WeChat**: zhcmason
- **Issues**: [GitHub Issues](https://github.com/mason0510/beyond-compare/issues)

## 📄 License

MIT License - see [LICENSE](LICENSE) for details

This project is licensed under MIT License. You are free to use, modify, and distribute this project, but you must retain the original copyright notice and license text.

## 🤝 Contributing

Contributions are welcome! Whether reporting issues, suggesting improvements, or submitting code, all help is appreciated.

Please refer to [CONTRIBUTING.md](CONTRIBUTING.md) for detailed contribution guidelines.

## Changelog

### v1.0.0 (2026-03-14)
- ✨ Initial release
- ✨ Side-by-side comparison view support
- ✨ VS Code Dark+ theme
- ✨ Multi-file switching functionality
- ✨ Complete statistics display
- ✨ Synchronized scroll support

See [CHANGELOG.md](CHANGELOG.md) for complete version history.

---

**Last Updated**: 2026-03-14
**Maintainer**: Mason ([@mason0510](https://github.com/mason0510))
