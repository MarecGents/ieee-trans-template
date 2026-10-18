# 中文期刊论文 LaTeX 模板（chinese-core）

> 基于 `ctexart` + XeLaTeX 的中文期刊论文模板：提供**单栏投稿稿**与**双栏定稿**两套版式，并支持 EPS 矢量图。

本模板与 `templates/ieee/`（IEEE Transactions，双栏）并列，面向中文期刊投稿：A4 版式、宋体小四正文、1.5 倍行距、GB/T 7714 顺序编码制参考文献，并保留 IEEE 模板中的常用宏包、修订标记（`\textdelet` / `\textadd`）与定理环境。

| 文件 | 版式 | 说明 |
|------|------|------|
| `PaperTemplate.tex` | 单栏投稿稿 | 默认版式，正文单栏排印 |
| `PaperTemplate-twocol.tex` | 双栏定稿 | 首页信息通栏、正文两栏；与单栏版共用 `mybib.bib` 与 `figure/` |

两套模板内容相同、文件独立，可分别编译，便于在“投稿稿”和“双栏排版稿”之间切换。

---

## 📁 目录结构

```
templates/chinese-core/
├── PaperTemplate.tex         # 单栏模板（ctexart + XeLaTeX）
├── PaperTemplate.pdf         # 单栏模板编译产物（可直接查看排版效果）
├── PaperTemplate-twocol.tex  # 双栏模板（首页通栏 + 正文两栏）
├── PaperTemplate-twocol.pdf  # 双栏模板编译产物
├── mybib.bib                 # 参考文献库（中文期刊/学位论文/会议/标准 + 英文 IEEE 期刊/会议/标准/专著）
├── citesort.sty              # 引用排序压缩样式（从 templates/ieee/ 复制，本模板未加载，原因见下文）
├── figure/                   # 示例图片目录（模板中实际引用）
│   ├── fig_sine.png          #   正弦波示意（子图 a）
│   ├── fig_damped.png        #   衰减正弦示意（子图 b）
│   └── fig_eps_demo.eps      #   EPS 矢量图示例
└── README.md                 # 本文件
```

> 说明：两份 `PaperTemplate*.pdf` 放在模板目录根下，与 `templates/ieee/PaperTemplate.pdf` 的组织方式保持一致。

---

## 🚀 快速开始

### 编译命令（推荐 latexmk）

```bash
cd templates/chinese-core
latexmk -xelatex PaperTemplate.tex          # 单栏版
latexmk -xelatex PaperTemplate-twocol.tex   # 双栏版
```

`latexmk` 会自动处理 `bibtex` 与多次编译（交叉引用、参考文献）。两个模板的 `.aux`、`.bbl` 等中间文件相互独立，互不影响。

或手动四步（需要运行 **bibtex**，否则参考文献显示为 `[?]`）：

```bash
# 单栏版
xelatex PaperTemplate.tex
bibtex  PaperTemplate
xelatex PaperTemplate.tex
xelatex PaperTemplate.tex

# 双栏版
xelatex PaperTemplate-twocol.tex
bibtex  PaperTemplate-twocol
xelatex PaperTemplate-twocol.tex
xelatex PaperTemplate-twocol.tex
```

⚠️ **推荐使用 XeLaTeX**（模板按 `fontspec` / `xeCJK` 中文字体方案设计）。`pdflatex` 也可经 CTeX 的 CJK 回退机制编译出 PDF，但字体、标点与版式不保证与 XeLaTeX 一致，故不作为推荐方式。

### 输出

编译完成后生成对应的 `PaperTemplate.pdf`（单栏）或 `PaperTemplate-twocol.pdf`（双栏）；`.aux`、`.log`、`.bbl` 等中间文件已在 `.gitignore` 中忽略，可随时删除。

---

## 🔤 字体说明

模板默认使用 **Windows 系统字体**：

```latex
\documentclass[UTF8, a4paper, zihao=-4, fontset=windows]{ctexart}
% 双栏版：\documentclass[UTF8, a4paper, zihao=-4, fontset=windows, twocolumn]{ctexart}
```

- `fontset=windows`：宋体（SimSun）、黑体（SimHei）、楷体（KaiTi）、仿宋（FangSong），需在 Windows 本机编译。
- **Overleaf / 无 Windows 字体的环境**：改用 TeX Live 自带的 Fandol 字体：

  ```latex
  \documentclass[UTF8, a4paper, zihao=-4, fontset=fandol]{ctexart}
  % 双栏版：\documentclass[UTF8, a4paper, zihao=-4, fontset=fandol, twocolumn]{ctexart}
  ```

- macOS 可用 `fontset=mac`，Linux 可配置 `fontset=ubuntu` 或 `fontset=fandol`。

---

## 📐 版式规格

| 项目 | 设置 | 实现方式 |
|------|------|----------|
| 纸张 / 页边距 | A4；上下 2.5 cm，左右 2.8 cm | `geometry` |
| 正文 | 宋体小四（12 bp），1.5 倍行距，首行缩进 2 字符 | `zihao=-4`、`\linespread{1.5}`、`\parindent=2em` |
| 中文题目 | 黑体三号居中 | 手动标题块 |
| 中文作者 | 楷体小四 | 手动标题块 |
| 中文单位 | 宋体小五 | 手动标题块 |
| 摘要 / 关键词 | 宋体五号；“摘要：”“关键词：”黑体 | 手动块 |
| 中图分类号 / 文献标志码 | 宋体五号（标签黑体） | 手动块 |
| 英文标题 / 作者 / 单位 / 摘要 / 关键词 | 依次为三号粗体、小四、小五、五号 | 手动块 |
| 一级标题 | 黑体四号 | `\ctexset{section/format=...}` |
| 二级标题 | 黑体小四 | `\ctexset{subsection/format=...}` |
| 三级标题 | 黑体五号 | `\ctexset{subsubsection/format=...}` |
| 图题 / 表题 | 五号黑体；**图题在下、表题在上** | `caption` 宏包 |
| 子图题 | 小五宋体 (a)(b)(c) | `subcaption` |
| 算法标题 | 五号黑体；“输入：/输出：”中文标签 | `algorithm` + `algpseudocode` |
| 参考文献 | 宋体小五，GB/T 7714 顺序编码制 | `gbt7714` + `gbt7714-numerical.bst` |
| 页码 | 页脚居中，五号 | `fancyhdr` |
| 定理类环境 | 中文名：定理 / 引理 / 推论 / 注 / 命题 | `amsthm` |

### 单栏版与双栏版的差异

| 项目 | `PaperTemplate.tex`（单栏） | `PaperTemplate-twocol.tex`（双栏） |
|------|------------------------------|-------------------------------------|
| 文档类选项 | `ctexart` | `ctexart` + `twocolumn` |
| 首页信息 | 全宽单栏排印 | `\onecolumn` 通栏排印 |
| 正文 | 单栏（版心宽约 15.4 cm） | 两栏（栏宽约 7.2 cm，栏间距 7 mm） |
| 图 / 表 | 按版心宽度 | 表格用 `\resizebox{\columnwidth}{!}{...}` 缩放到栏宽，图片使用 `\linewidth`（即栏宽） |
| 长公式 | 原始宽度 | 按栏宽重排（式 (4) 的约束逐行排列） |
| 参考文献 | 两端对齐 | 窄栏内左对齐（`\raggedright`），避免过大的字距 |
| 首页脚注 | `\blfootnote`（基金项目 / 作者简介） | 同样使用 `\blfootnote`，排在通栏首页底部 |
| 典型用途 | 期刊投稿稿、单栏 PDF 稿 | 双栏定稿、双栏排版效果预览 |

---

## 📦 已复用 / 新增的宏包

从 `templates/ieee/` 复用（保持原有功能）：

| 类别 | 宏包 |
|------|------|
| 数学 | `amsmath`, `amssymb`, `bm` |
| 表格 | `multirow`, `booktabs`, `diagbox` |
| 图片 | `graphicx`, `subcaption`, `epstopdf`（仅 pdfLaTeX 路径加载，见“EPS 图片支持”） |
| 算法 | `algorithm`, `algpseudocode` |
| 定理 | `amsthm`, `mdframed` |
| 版式 | `comment`, `url`, `xcolor` |

因中文排版需要新增：

| 宏包 | 用途 |
|------|------|
| `ctexart`（文档类） | 中文文档类、字号（`\zihao`）、宋/黑/楷/仿字体切换 |
| `geometry` | A4 与页边距 |
| `fancyhdr` | 页脚居中页码 |
| `caption`（由 `subcaption` 载入） | 图表标题字体、位置 |
| `etoolbox` | `\AtBeginEnvironment` 设置参考文献字号 |
| `iftex` | 按编译器条件加载 `epstopdf`（XeLaTeX 下无需该宏包） |
| `hyperref` | 交叉引用与 PDF 书签（`bookmarksnumbered`；`hidelinks` 使引用无彩色边框） |
| `gbt7714` | GB/T 7714 参考文献样式（内部会加载 `natbib`） |

**未复用**的 IEEE 模板宏包：`balance`（双栏末页均衡，本模板用 `\raggedbottom` 控制末页）、`inputenc`（XeLaTeX 原生 UTF-8）、`cite` / `citesort`（见下节）。

---

## 🖼️ EPS 图片支持

模板支持在 `figure/` 中直接使用 `.eps` 矢量图：

```latex
\begin{figure}[htbp]
  \centering
  \includegraphics[width=0.7\linewidth]{figure/fig_eps_demo.eps}
  \caption{EPS 矢量图示例}\label{fig:epsdemo}
\end{figure}
```

`figure/fig_eps_demo.eps` 是随模板提供的示例文件；两个模板的图片区都有一段被注释掉的 EPS 示例，取消注释即可编译查看。

EPS 在不同编译器下的处理方式：

| 编译器 | 转换链路 | 依赖 |
|--------|----------|------|
| XeLaTeX（推荐） | `graphicx` 的 `xetex.def` 通过 `\special{PSfile=...}` 调用 Ghostscript，把 EPS 转成 PDF 图形 | Ghostscript |
| pdfLaTeX | `epstopdf` 宏包在编译时自动调用 Ghostscript 完成转换 | Ghostscript |

- **Ghostscript 要求**：上述转换都需要 Ghostscript。TeX Live 自带 Ghostscript（Windows 位于 `tlpkg/tlgs/bin/`，通常无需单独安装，编译时会自动找到）；Overleaf 等在线平台也自带 Ghostscript。
- **检查 Ghostscript**：命令行执行 `gs --version`（macOS / Linux）或 `gswin64c --version`（Windows 且 Ghostscript 在 `PATH` 中），能输出版本号即可；Windows 的 TeX Live 环境通常可直接运行 `rungs --version`（TLGS，随 TeX Live 安装，编译时会自动使用）。
- **Ghostscript 不可用时**：
  1. 安装 Ghostscript 并加入 `PATH`（TeX Live 安装时勾选 tlgs 组件也可）；
  2. 或在命令行手动转换：`epstopdf figure/fig_eps_demo.eps`（TeX Live 自带该命令，生成同名 PDF），再改为引用 `.pdf` 文件；
  3. 或改用 PDF / PNG / JPG 格式的同一张图。
- **格式建议**：EPS / PDF 适合矢量曲线与示意图，照片建议用 PNG / JPG；`\includegraphics` 不写扩展名时，`graphicx` 会按 `.pdf`、`.png`、`.jpg`、`.eps` 的顺序查找同名文件，写全扩展名可避免误选。

---

## 🧩 双栏模板（`PaperTemplate-twocol.tex`）

双栏版与单栏版共用同一套示例内容、`mybib.bib` 与 `figure/`，区别在于版式与少量排版处理：

### 实现方式

- **文档类**：`\documentclass[UTF8, a4paper, zihao=-4, fontset=windows, twocolumn]{ctexart}`。
- **首页信息**：首页用 `\onecolumn` 按通栏排印标题、作者、单位、中英文摘要与关键词；基金项目 / 作者简介用 `\blfootnote` 排到首页底部；之后用 `\twocolumn` 切换到两栏正文。
- **栏宽设置**：`\setlength{\columnsep}{7mm}`，并用 `\raggedbottom` 避免末页被纵向拉伸。
- **表格**：表 1、表 2（`diagbox`）在栏宽内放不下，统一用 `\resizebox{\columnwidth}{!}{...}` 缩放到栏宽。
- **长公式**：式 (4) 的约束按栏宽逐行重排，变量范围在公式后的正文中说明。
- **算法**：算法 1 作为双栏浮动体排入单栏。
- **参考文献**：窄栏内使用 `\raggedright` 左对齐，避免两端对齐时出现过大字距或 `Underfull` 提示。
- **图片**：`\includegraphics` 的 `width` 用 `\linewidth` 即可自动取栏宽；双子图示例已按 `0.47\linewidth` 排布。

### 编译

```bash
cd templates/chinese-core
latexmk -xelatex PaperTemplate-twocol.tex
```

### 使用提示

- 双栏版正文按栏宽排印，**新增宽表或长公式时需检查是否越界**：可优先用 `\resizebox{\columnwidth}{!}{...}`、`aligned` 拆分、`\small` 或精简表头 / 公式。
- 示例首页信息较长，正文从第 2 页开始；实际论文摘要较短时通栏区会相应变短，正文会更早进入两栏。若期刊要求正文紧接摘要，可缩短摘要或调小首页各段间距（`\vspace{...}`）。
- 双栏正文中的 `\blfootnote` 显示位置与单栏不同；基金项目 / 作者简介应放在 `\twocolumn` 之前的通栏区。
- 若某期刊要求参考文献两端对齐，可把 `\AtBeginEnvironment{thebibliography}` 中的 `\raggedright` 改为 `\sloppy`。
- 只需单栏版时直接使用 `PaperTemplate.tex`，两者互不依赖。

---

## ⚠️ 关于 `cite` / `citesort`

- `gbt7714` 内部会 `\RequirePackage{natbib}`（GB/T 7714 顺序编码制所需的引用机制）。
- `natbib` 官方声明**不应与 `cite` 同用**：导言区同时加载 `cite` 会触发
  `Package natbib Warning: The 'cite' package should not be used with natbib...`，
  且最终的排序与压缩实际由 `natbib` 完成，`cite` 不起作用。
- `citesort.sty` 直接改写 LaTeX 内部的 `\@citex`，与 `natbib`（`gbt7714`）的引用处理相互覆盖，属于硬冲突。
- 因此本模板**不加载 `cite` 与 `citesort`**；`[1,2,3]→[1-3]` 的排序压缩由 `gbt7714` 对 `natbib` 的设置（`\NAT@cmprs=1`）等价提供，正文引用显示为 `[1]`、`[2-4]` 形式。
- `citesort.sty` 仍随模板附带一份（从 `templates/ieee/` 复制），便于将来改回 `IEEEtran` 时继续使用。

---

## ✍️ 使用说明（需要修改的位置）

1. **首页信息**（`\begin{document}` 之后）：
   - 中文题目、作者、单位；
   - 基金项目、作者简介（`\blfootnote{...}`，首页无标记脚注）；
   - 中文摘要、关键词、中图分类号、文献标志码；
   - 英文题目、作者、单位、Abstract、Keywords。
   - 双栏版：以上内容位于 `\onecolumn` 与 `\twocolumn` 之间的通栏区。
2. **PDF 元信息**：`\hypersetup{pdftitle=..., pdfauthor=..., pdfkeywords=...}`，建议与标题一致。
3. **正文**：直接替换示例章节内容即可；模板已演示章节、`align`、`equation`、图（含 `subcaption` 子图）、三线表（`multirow`）、`diagbox` 表、`algorithm` 伪代码、交叉引用（`\eqref`/`\ref`）、`mdframed` 文本框。
4. **修订标记**：`\textdelet{删除的文字}`（红色）、`\textadd{新增的文字}`（蓝色），与 IEEE 模板同名同用法，投稿前可全局关闭或删除。
5. **图片**：放入 `figure/` 目录，修改 `\includegraphics{...}` 文件名即可；支持 PNG / JPG / PDF / EPS，EPS 用法见上文“EPS 图片支持”。
6. **参考文献**：编辑 `mybib.bib`，中文条目**必须**加 `language = {zh}`；作者之间用 `and` 分隔；未在正文中 `\cite` 的条目不会出现在参考文献表中（示例库中的 `gb18030` 即未引用）。
7. **双栏版**：如同时维护单栏与双栏两套稿子，修改正文后注意同步 `PaperTemplate.tex` 与 `PaperTemplate-twocol.tex`；双栏版新增内容后按栏宽检查图表/公式。

### 参考文献条目类型（`gbt7714-numerical.bst` 已支持）

| 类型 | 示例 |
|------|------|
| 中文期刊 | `@article` + `language={zh}` |
| 中文学位论文 | `@phdthesis` / `@mastersthesis` |
| 中文会议 | `@inproceedings` |
| 标准 | `@standard`（含 `number` 字段，如 `GB 18030--2022`） |
| 英文期刊 / 会议 | `@article` / `@inproceedings`（不加 `language`） |
| 英文专著 | `@book` |

---

## ❓ 常见问题

| 现象 | 原因与处理 |
|------|-----------|
| 中文不显示 / 乱码 | 用了 `pdflatex`，改用 `xelatex` 或 `latexmk -xelatex` |
| 日志出现 `Missing character` | 字体集与环境不匹配：Windows 用 `fontset=windows`，无 Windows 字体改用 `fontset=fandol` |
| 参考文献显示 `[?]` | 未运行 `bibtex`，或编译次数不足（按上面四步流程；`latexmk` 会自动处理） |
| Overleaf 编译报字体错误 | 把 `fontset=windows` 改为 `fontset=fandol`，并上传 `figure/`、`mybib.bib`、`citesort.sty` |
| 图片找不到 | 确认图片在 `figure/` 下，且文件名与 `\includegraphics[...]{figure/xxx}` 一致 |
| EPS 图片编译报错（Ghostscript 相关） | 环境缺少可执行的 Ghostscript：安装 Ghostscript 或使用 TeX Live 自带的 TLGS；也可先 `epstopdf` 转成 PDF 再插入 |
| 双栏版出现 `Overfull \hbox` | 长公式 / 宽表格超出栏宽：用 `\resizebox{\columnwidth}{!}{...}`、`aligned` 拆分公式、`\small` 或缩短表头 |
| 双栏版首页脚注不显示 | 基金项目 / 作者简介须放在 `\onecolumn` 与 `\twocolumn` 之间的通栏区，并使用 `\blfootnote` |
| 想改期刊格式 | 直接改文中 `\zihao{...}`、`\ctexset`、`caption` 设置即可，均为显式命令 |

---

## 📌 重要提醒

1. 本模板用于**论文写作与生成 PDF 稿**；不同期刊在字号、行距、图表标题、参考文献格式上存在差异，**是否接受 LaTeX 投稿、最终格式要求以目标期刊官方投稿指南为准**，请按指南做必要微调。
2. 模板中的论文内容（题目、作者、摘要、数据、结论）以及 `mybib.bib` 中的参考文献条目均为示例占位（部分文献信息为虚构，请勿直接引用），投稿前请全部替换为真实内容与文献。
3. 单栏版与双栏版共用 `mybib.bib`、`figure/` 与 `citesort.sty`，只在本目录内自洽，不依赖 `templates/ieee/` 中的任何文件。
4. EPS 图片的转换依赖 Ghostscript；在不提供 Ghostscript 的编译环境中，请改用 PDF / PNG / JPG 图片。

---

*License 与维护信息见仓库根目录 `README.md`。*
