# TeX-Tools

**_最后更新时间：2024-10-5_**

Here are some of my practical tips and tools for using LaTeX.

这里收集了我使用 LaTeX 的各种使用建议和实用工具。

## 编译引擎

- `pdflatex`

  这个引擎是三类引擎中速度最快的。

  如果你**只使用英语这一种语言**且**不在意字体**，仅在这一种情况下，推荐使用这个引擎。

- `xelatex`

  这个引擎，是很多网上教程推荐使用的，但是我并不是很推荐。不可否认的是，我一开始写 LaTeX 中文笔记时，也是使用这个引擎。但是 xelatex 和其他两种本身不是属于同一个分支的产物，很多宏包在不同引擎中切换会出现了很多警告和报错。

- `lualatex`

  这个引擎（应该）是三类引擎中速度最慢的。但也是我最推荐的引擎，无论你使用哪种语言。

  我使用这个引擎其实不是很长时间，在之前，我一直使用 pdflatex 引擎（是的，我很少用 LaTeX 写中文的文档）我从 pdflatex 切换过来，仅仅是修改了字体相关的宏包就可以无缝衔接使用了。

- `latexmk`

  这不是一个严格意义上的编译引擎，它是一个类似于 Makefile 的 LaTeX 自动化构建工具。但是它的速度是非常慢的，尤其是在构建大型文档项目的时候。急性子（e.g. Me）不推荐使用。

## 必要的宏包

LaTeX 的使用群体绝大多数的共同需求就是需要输入数学公式。以下这五个是我使用很久的数学公式符号的宏包。

- `amsmath`, `amssymb`, `amsthm`
- `amsfonts`
- `mathtools`

如果你和我一样，以上五个宏包都要使用。请将它们这样放置在文档的合适位置（警告：千万不要更改它们其中任何一个的顺序！否则你会像过去的我一样，被迫去 tex stack exchange 找解决方法）

```latex
\usepackage{amsmath,amssymb,amsthm}
\usepackage{amsfonts}
\usepackage{mathtools}
```

- `microtype`

  调整字母间间隔的宏包。目前仅支持 pdflatex（lualatex 实测也有效），部分支持 xelatex。

### 页面布局

- `geometry`

  纸张大小，页面布局设置

- `fancyhdr`

  页首页脚设置

### 定理环境

- `thmtools`

  推荐使用这个宏包来定义更精细的定理环境，而不要使用 `ntheorem`。

- `tcolorbox`

  这个其实和定理环境没啥关系，它主要是提供一个颜色盒子。使得你的环境变得五（花）彩（里）斑（胡）斓（哨）。

### 超链接

- `hyperref`

  这是一个生成超链接引用宏包。例如目录，定理引用等各种在 PDF 中需要超链接进行跳转的都可以使用它。

- `bookmark`

  书签宏包。一般搭配 `hyperref` 进行使用。

### 颜色

- `color` 和 `xcolor`

  建议两个宏包一起使用，这样基本能覆盖大部分颜色。如果你对颜色还有更高的要求，我推荐你去[这里](https://latexcolor.com/)寻找你感兴趣的颜色。

### 字体

- `inputenc`和 `fontenc`

  这两个宏包是在 pdflatex 上使用的。

- `fontspec`

  本身对字体支持友好的 xelatex 和 lualatex 都可以使用。

### 中文支持

- `ctex`

  这个宏包是我目前用过最好的中文宏包了。不推荐使用 `xeCJK`。

  如果你是在文档中**少量使用中文**（即文档的主要语言不是中文），请使用设置一下命令选项：

  ```latex
  \usepackage[scheme=plain]{ctex}
  ```

### 多语言支持

主要有两个宏包 `babel` 和 `polyglossia`。我两个宏包都使用过（我文档中有时会使用到三种语言，分别是中文，英语和法语），这两个宏包都是经常更新的。

- `babel`

  比较推荐使用这个。无论是 xelatex 还是在 lualatex 上，这个宏包都能很好地实现功能。

- `polyglossia`

  这个使用文档写得比较好。但是一旦出现问题，去 tex stack exchange 求助的时候，有很多人都会建议你使用 `babel`，我也不知道为什么。反正看个人需求吧，其实看文档基本也可以修复大部分问题。只要少数涉及 LaTeX 排版底层的东西才会去 stack exchange 寻求解决。

### 画图

对于在 LaTeX 上实现画图功能，我建议大家不要插入图片或插入 PDF，而是使用以下宏包画矢量图。

- `tikz`

  能画各种矢量图。详情请看使用文档（上千页的使用文档，我几句话是无法表达清楚的）

- `pgfplots`

  一般用于画函数图像。

### 条目

- `enumitem`

  有序条目和无序条目都可以实现自定义。

## Others

- `de-macro`

  这是一个可以修改命令的 Python 脚本（**不是 LaTeX 宏包！**）。它可以**将自定义命令恢复成 LaTeX 的原有命令**（当然还有其他功能，我主要使用的是这个功能）

  目前最新版的 TeXLive2024 已将它移除，所以，要使用它只能去 [CTAN 上的地址](https://ctan.org/tex-archive/support/de-macro)下载，然后自己操作。

## 更高级的功能

编写 sty 和 cls 使用的宏包

- `iftex`

  功能和宏包名称一样。提供 `if...then...` 语法，我使用它实现引擎之间的判断，也就是在使用不用引擎的时候会调用不同的宏包，避免报错。
