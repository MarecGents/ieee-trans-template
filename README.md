# IEEE Trans Template

> LaTeX templates for IEEE Transactions and Chinese core journals

本仓库提供两套开箱即用的 LaTeX 模板，适合通信、信号处理、计算机等工程领域的论文写作：

| 模板目录 | 适用场景 | 版式 | 推荐编译器 |
|----------|----------|------|------------|
| `templates/ieee/` | IEEE 期刊 / 会议投稿 | journal 双栏（可切换 conference / onecolumn） | pdfLaTeX |
| `templates/chinese-core/` | 中文核心期刊写作与 PDF 稿 | 单栏投稿稿 + 双栏定稿 | XeLaTeX |

两套模板均包含完整的模板源码、编译产物 PDF 与参考文献库；IEEE 模板的使用说明见本文件，中文模板另附独立的 [使用说明](templates/chinese-core/README.md)。

---

## 📁 目录结构

```
ieee-trans-template/
├── templates/                  # 论文模板目录（按期刊名分层）
│   ├── ieee/                   # IEEE Transactions 模板
│   │   ├── PaperTemplate.tex   # 主模板文件 (IEEEtran, journal 双栏)
│   │   ├── PaperTemplate.pdf   # 编译产物
│   │   ├── mybib.bib           # 参考文献库（预置 30+ IEEE 期刊缩写）
│   │   └── citesort.sty        # 引用排序与压缩样式
│   ├── chinese-core/           # 中文核心期刊模板（ctexart + XeLaTeX）
│   │   ├── PaperTemplate.tex   # 单栏模板（投稿稿）
│   │   ├── PaperTemplate.pdf   # 单栏模板编译产物
│   │   ├── PaperTemplate-twocol.tex  # 双栏模板（首页通栏 + 正文两栏）
│   │   ├── PaperTemplate-twocol.pdf  # 双栏模板编译产物
│   │   ├── mybib.bib           # 参考文献库（GB/T 7714，中英文示例）
│   │   ├── citesort.sty        # 从 ieee 复制（本模板未加载，原因见其 README）
│   │   ├── figure/             # 示例图片目录（含 EPS 示例 fig_eps_demo.eps）
│   │   └── README.md           # 中文模板使用说明（含 EPS / 双栏说明）
│   ├── elsevier/               # 📌 未来扩展
│   └── acm/                    # 📌 未来扩展
├── .gitignore                  # LaTeX 编译产物忽略规则
├── LICENSE                     # MIT License
└── README.md                   # 本文件
```

---

## 🚀 快速开始

### 编译 IEEE 模板（`templates/ieee/`）

使用标准的 `pdflatex` + `bibtex` 编译流程：

```bash
# 1. 进入对应期刊模板目录
cd templates/ieee

# 2. 编译主文档（需 2-3 次以解析交叉引用）
pdflatex PaperTemplate.tex
bibtex PaperTemplate
pdflatex PaperTemplate.tex
pdflatex PaperTemplate.tex
```

或使用 `latexmk` 一键编译（推荐）：

```bash
cd templates/ieee
latexmk -pdf PaperTemplate.tex
```

### 编译中文模板（推荐 XeLaTeX）

中文模板位于 `templates/chinese-core/`，按 `ctexart` + `fontspec`/`xeCJK` 方案设计，**推荐使用 XeLaTeX**（`pdflatex` 虽可经 CTeX 的 CJK 回退编译，但字体、标点与版式不保证一致）。提供单栏投稿稿与双栏定稿两套模板：

```bash
cd templates/chinese-core
latexmk -xelatex PaperTemplate.tex          # 单栏版（推荐）
latexmk -xelatex PaperTemplate-twocol.tex   # 双栏版
# 或手动四步（单栏版）：
# xelatex PaperTemplate.tex
# bibtex  PaperTemplate
# xelatex PaperTemplate.tex
# xelatex PaperTemplate.tex
```

两版共用 `mybib.bib` 与 `figure/`，`.aux`、`.bbl` 等中间文件相互独立。中文模板的字体、版式、EPS 图片支持与双栏说明详见 [中文模板 README](templates/chinese-core/README.md)。

### 切换文档模式

`PaperTemplate.tex` 顶部提供了三种 IEEEtran 模式：

```latex
%\documentclass[conference]{IEEEtran}           % IEEE 会议版本
\documentclass[journal]{IEEEtran}               %% IEEE 期刊双栏版本（默认）
%\documentclass[12pt, draftclsnofoot, onecolumn]{IEEEtran}  % 期刊单栏版本
```

取消对应行的注释即可切换。

---

## 🔧 工具与环境

### 编译环境

本模板依赖 **LaTeX 完整发行版**，以下两种任选其一：

| 发行版 | 说明 | 下载 |
|--------|------|------|
| **TeX Live** ⭐ 首选推荐 | 跨平台（Windows / macOS / Linux），宏包最全，官方维护。安装包较大（约 4–7 GB），安装耗时较长。 | [texlive2026.iso](https://mirror.ctan.org/systems/texlive/Images/) |
| **CTeX** | Windows 原生中文支持，基础版可快速上手。完整版同样安装缓慢，不同版本安装步骤有细微差异。 | [CTeX 下载页](https://ctex.org/CTeX/download/#latest) |

> 💡 TeX Live 是绝大多数期刊和会议的投稿编译环境，强烈建议优先安装。

### 写作与编译工具

| 工具 | 适用平台 | 说明 |
|------|----------|------|
| **WinEdt** ⭐ | Windows | 作者首选推荐，与 IEEEtran 模板配合极佳，支持自动补全、拼写检查、DVI/PDF 预览。[下载地址](https://www.winedt.com/download.html) |
| **VS Code** | Windows / macOS / Linux | 免费开源的跨平台编辑器，安装 [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) 插件后即可编译 LaTeX。[下载地址](https://code.visualstudio.com/)。**注意：** VS Code 对 CTeX 适配较差，建议搭配 TeX Live 使用 |
| **Overleaf** | Web (在线) | 最流行的在线协作 LaTeX 平台，无需本地安装，支持实时预览和多人协作。[官网链接](https://www.overleaf.com/)。可直接上传本模板压缩包开始写作 |
| **TeXstudio** | Windows / macOS / Linux | 开源 LaTeX IDE，内置公式预览、代码折叠、语法高亮，对中文支持良好。[下载地址](https://www.texstudio.org/) |
| **LyX** | Windows / macOS / Linux | 所见即所得（WYSIWYM）的 LaTeX 前端，适合初学者快速上手。[下载地址](https://www.lyx.org/Download) |
| **TeXworks** | Windows / macOS / Linux | TeX Live 自带编辑器，轻量简洁，零配置启动。[项目主页](https://tug.org/texworks/) |

预置了覆盖通信、信号处理、无线网络、计算机等领域的常用期刊/会议缩写：

| 领域 | 期刊/会议 |
|------|-----------|
| **综合旗舰** | Proceedings of the IEEE |
| **通信** | IEEE Trans. Commun., IEEE Commun. Lett., IEEE Wireless Commun. Lett., IEEE J. Sel. Areas Commun., IEEE Trans. Wireless Commun., IEEE Trans. Veh. Technol. |
| **信号处理** | IEEE Trans. Signal Process., IEEE Signal Process. Lett., IEEE J. Sel. Top. Signal Process. |
| **物联网/网络** | IEEE Internet Things J., IEEE Trans. Netw. Sci. Eng., IEEE Trans. Cogn. Commun. Netw. |
| **安全** | IEEE Trans. Inf. Forensics Security |
| **移动计算** | IEEE Trans. Mob. Comput. |
| **杂志/教程** | IEEE Commun. Mag., IEEE Veh. Technol. Mag., IEEE Signal Process. Mag., IEEE Commun. Surveys Tutorials |
| **会议** | ICC, GLOBECOM, WCNC, WCSP, ICCS |
| **其他** | IEEE Access, IEEE Systems J., China Science: Information Science, EURASIP J. WCN |

所有缩写遵循 IEEE 官方规范，可直接在论文中引用。

---

## 📦 已加载的 LaTeX 包（`templates/ieee/`）

IEEE 模板预载了以下常用包，覆盖论文写作的主要需求；中文模板的宏包清单见 [中文模板 README](templates/chinese-core/README.md)：

| 类别 | 包 |
|------|-----|
| **数学** | `amsmath`, `amssymb`, `amsthm`, `bm` |
| **定理环境** | Theorem, Lemma, Corollary, Remark, Proposition |
| **表格** | `multirow`, `diagbox`, `booktabs` |
| **图片** | `graphicx`, `subcaption`, `epstopdf` |
| **算法** | `algorithm`, `algpseudocode` |
| **引用** | `cite`, `citesort` |
| **版式** | `balance`, `mdframed`, `comment`, `url`, `xcolor` |

---

## 🇨🇳 中文期刊模板（chinese-core）

`templates/chinese-core/` 面向中文核心期刊（通信 / 电子信息）的写作与排版，基于 `ctexart` + **XeLaTeX**，与 IEEE 模板并列使用。提供单栏投稿稿与双栏定稿两套模板，并支持 PNG / JPG / PDF / EPS 图片；EPS 转换依赖 Ghostscript（TeX Live 自带）。详见 [中文模板 README](templates/chinese-core/README.md)。

| 项目 | 说明 |
|------|------|
| 版式 | `PaperTemplate.tex`：A4 单栏投稿稿；`PaperTemplate-twocol.tex`：A4 双栏定稿（首页信息通栏、正文两栏） |
| 首页信息 | 中英文题目 / 作者 / 单位 / 摘要 / 关键词、中图分类号、文献标志码、基金项目、作者简介 |
| 标题层级 | 一级黑体四号、二级黑体小四、三级黑体五号 |
| 图表 | 图题在下、表题在上（五号黑体）；三线表、`multirow`、`diagbox`、`subcaption` 子图；双栏版表格按栏宽缩放 |
| 图片格式 | PNG / JPG / PDF / EPS（EPS 需 Ghostscript；XeLaTeX 与 pdfLaTeX 均可） |
| 参考文献 | GB/T 7714 顺序编码制（`gbt7714` + BibTeX），中文条目需 `language = {zh}` |
| 复用 IEEE 宏包 | `amsmath`、`amssymb`、`bm`、`graphicx`、`subcaption`、`multirow`、`booktabs`、`diagbox`、`algorithm`、`algpseudocode`、`amsthm`、`mdframed`、`xcolor`、`comment`、`url` |
| 其他 | `\textdelet`（红）/ `\textadd`（蓝）修订标记、中文定理/引理/推论/注/命题环境、中文算法伪代码、`hyperref` 无边框交叉引用（`hidelinks`）、双栏/单栏两套模板 |

⚠️ **投稿方式提醒（重要）**：中文核心期刊多数要求按本刊 Word 模板撰写 / 上传 docx，LaTeX 通常不是官方投稿格式；是否接受 LaTeX、需要哪些文件类型、参考文献与版式细节，**均以目标期刊官方投稿指南为准**。本模板用于写作与生成 PDF 稿，请按目标期刊要求准备投稿材料。

---

## 🎯 兼容期刊（`templates/ieee/`）

IEEE 模板基于 **IEEEtran** 文档类，支持 **全部 IEEE 期刊与会议** 的投稿格式。切换 `journal`/`conference` 模式即可适配。以下是各领域的代表性期刊：

| 领域 | 知名期刊 |
|------|----------|
| **通信与网络** | IEEE Trans. Commun. (TCOM), IEEE J. Sel. Areas Commun. (JSAC), IEEE Trans. Wireless Commun. (TWC), IEEE/ACM Trans. Netw. (TON), IEEE Commun. Mag. |
| **信号处理** | IEEE Trans. Signal Process. (TSP), IEEE Signal Process. Mag. (SPM), IEEE/ACM Trans. Audio Speech Lang. Process. (TASLP) |
| **信息论** | IEEE Trans. Inf. Theory (TIT) |
| **计算机视觉与AI** | IEEE Trans. Pattern Anal. Mach. Intell. (TPAMI), IEEE Trans. Neural Netw. Learn. Syst. (TNNLS), IEEE Trans. Image Process. (TIP) |
| **控制系统** | IEEE Trans. Autom. Control (TAC), IEEE/CAA J. Autom. Sin. |
| **电力与能源** | IEEE Trans. Power Syst. (TPWRS), IEEE Trans. Smart Grid (TSG) |
| **移动计算与IoT** | IEEE Trans. Mob. Comput. (TMC), IEEE Internet Things J. (IoT-J) |
| **信息安全** | IEEE Trans. Inf. Forensics Security (TIFS) |
| **综合旗舰** | Proc. IEEE, IEEE Access |
| **教程/杂志** | IEEE Commun. Surv. Tutor. (COMST), IEEE Signal Process. Mag., IEEE Veh. Technol. Mag. |
| **会议** | ICC, GLOBECOM, INFOCOM, ICASSP, CVPR, WCNC |

> 💡 如需向 IEEE 会议投稿，取消 `PaperTemplate.tex` 第 1 行注释、注释掉第 2 行即可切换为 `conference` 模式。

---

## 📄 许可证

[MIT License](LICENSE) © 2026 MarecGents

---

## 👤 维护信息

### 模板维护者

**陶星伦（MarecGents）**

- 北京信息科技大学 信息与通信工程方向 在读硕士研究生
- 导师：岳新伟 教授
- GitHub：[@MarecGents](https://github.com/MarecGents)

**岳新伟 教授** (Senior Member, IEEE)

- 北京信息科技大学 信息与通信工程学院 副院长、教授
- 2018 年博士毕业于北京航空航天大学，2024 年起任教授
- 研究方向：6G 网络、非正交多址（NOMA）、智能超表面（RIS）、物理层安全、近场通信、卫星通信跳束
- 入选 2023/2024 年全球前 2% 顶尖科学家榜单
- 获 2024 年第十七届北京青年优秀科技论文奖
- 担任 IEEE Systems Journal 等期刊编委
- [个人主页](https://tx.bistu.edu.cn/xkjs/dsjj/e8859feaeaf34f58a2a17a14e2c245dd.htm)

---

*本模板服务于学术论文写作，欢迎使用和贡献。*
