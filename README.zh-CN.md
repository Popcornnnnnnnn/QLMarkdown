# QLMarkdown

[English](README.md) · **简体中文**

> 本仓库是 [sbarex/QLMarkdown](https://github.com/sbarex/QLMarkdown) 的 Fork。本文件提供简体中文导读；完整选项、FAQ 和最新发布信息请以[英文 README](README.md)及上游仓库为准。

QLMarkdown 是一款 macOS 应用，主要提供：

- 在 Quick Look 中预览 Markdown 文件；
- 通过实验性的 Shortcuts 扩展把 Markdown 转换成 HTML；
- 用命令行工具批量把 Markdown 转换成 HTML；
- 通过图形界面配置 Quick Look 预览样式。

> QLMarkdown 不是独立的 Markdown 编辑器或常规阅读器。
>
> 软件按“现状”提供，不附带任何形式的保证。

除了 `.md`，Quick Look 扩展还可以预览 `.rmd`、`.mdx`、`.mdc`、`.qmd`、`.apib`、TextBundle 包和 `.mermaid` 文件。R Markdown 不会执行 R 代码，MDX 也不会渲染 JSX。

## 截图

### Quick Look 预览

![Quick Look 界面](./assets/img/preview_quicklook.png)

### Shortcuts 命令

![Shortcuts 界面](./assets/img/preview_shortcut.png)

## 安装

可以从[上游 Release 页面](https://github.com/sbarex/QLMarkdown/releases)下载最新构建，也可以通过 Homebrew 安装：

```shell
brew install --cask qlmarkdown
```

预编译应用已经签名并通过 Apple 公证。

安装后必须至少启动一次应用，系统才会发现 Quick Look 扩展，并安装 Shortcuts 扩展需要的共享文件。之后可以在系统设置的扩展列表中确认 Quick Look 扩展已启用。

支持文件保存在：

```text
~/Library/Group Containers/group.org.sbarex.qlmarkdown
```

应用可能覆盖该目录中 `highlight` 和 `js` 子目录的内容。

## 卸载

将应用拖入废纸篓即可卸载。如需同时清理支持文件，可以删除：

```text
~/Library/Group Containers/group.org.sbarex.qlmarkdown
```

## Markdown 处理能力

QLMarkdown 基于 [`cmark-gfm`](https://github.com/github/cmark-gfm)，并增加了多种扩展：

- Emoji shortcode；
- 标题锚点；
- `==高亮==`；
- 将本地图片嵌入预览；
- 下标与上标；
- MathJax 数学公式；
- Mermaid 图表；
- 代码语法高亮；
- YAML 文件头。

它与 GitHub Markdown 的主要差异是源码高亮实现不同，因此配色、语言识别和部分排版细节可能不完全一致。

## Quick Look 设置

启动主应用后，可以选择 CSS 主题、基础字号、Markdown 选项和扩展，并用内置编辑器即时测试。要让设置生效，请使用 `Command-S` 或菜单中的 **File > Save settings**，也可以启用自动保存。

![主界面](./assets/img/main_interface.png)

常用功能包括：

- 浅色与深色主题，以及自定义 CSS；
- 智能引号、脚注、换行方式和 UTF-8 校验；
- 表格、任务列表、删除线、上下标和自动链接；
- Emoji、数学公式、Mermaid 和代码高亮；
- 将 Markdown 中引用的本地图片嵌入 Quick Look 输出；
- `.rmd` 和 `.qmd` 的 YAML 文件头渲染。

启用 Raw HTML 会允许渲染原始 HTML 和部分不安全链接，应只用于可信文档。更完整的选项说明见[英文 README](README.md#quick-look-settings)。

## 命令行工具

`qlmarkdown_cli` 位于 `QLMarkdown.app/Contents/Resources`，不要把可执行文件单独移出应用包。可以在应用菜单中创建符号链接，也可以手动执行：

```sh
ln -s /Applications/QLMarkdown.app/Contents/Resources/qlmarkdown_cli /usr/local/bin/qlmarkdown_cli
```

查看完整参数：

```sh
qlmarkdown_cli --help
```

CLI 支持批量转换、浅色/深色外观、字号、HTML 输出路径，以及大部分 Markdown 扩展。CLI 不会与主应用或 Quick Look 扩展共享设置。

## Shortcuts 命令

应用提供两个实验性 Shortcuts 命令：

- `Markdown format`：格式化 Markdown 并输出 HTML 字符串；
- `Markdown convert`：格式化 Markdown 并把 HTML 保存到文件。

## 从源码构建

克隆仓库后需要初始化子模块：

```sh
git submodule update --init
```

Sparkle、Yams 和 SwiftSoup 由 Swift Package Manager 管理。源码还依赖 `highlight`、PCRE2/JPCRE2、MathJax、Mermaid 和 `cmark-gfm`。构建 PCRE2 与 `cmark-gfm` 所需工具可以通过 Homebrew 安装：

```sh
brew install autoconf automake libtool cmake
```

## 安全说明

QLMarkdown 不会收集系统信息或被处理文件的内容。

为了让 Quick Look 能预览本地图片，应用和扩展包含读取系统文件的权限例外。只应使用可信来源的 Markdown 文档，尤其是在启用 Raw HTML、外部 JavaScript 库或本地图片嵌入时。

如果 Quick Look 预览未生效，请先在 **System Settings > General > Login Items & Extensions > Quick Look** 中确认 QLMarkdown 已启用。完整排查步骤见[英文 FAQ](README.md#faq)。
