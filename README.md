# IEEE Trans Template

> A LaTeX Template for IEEE Transactions

一篇开箱即用的 IEEE 期刊论文 LaTeX 模板，适合作为通信、信号处理、计算机等工程领域论文写作的起点。

---

## 📁 目录结构

```
ieee-trans-template/
├── templates/                  # 论文模板目录（按期刊名分层）
│   ├── ieee/                   # IEEE Transactions 模板
│   │   ├── PaperTemplate.tex   # 主模板文件 (IEEEtran, journal 双栏)
│   │   ├── mybib.bib           # 参考文献库（预置 30+ IEEE 期刊缩写）
│   │   ├── citesort.sty        # 引用排序与压缩样式
│   │   ├── figure/             # 图片资源目录
│   │   └── pdf/                # PDF 输出目录
│   ├── elsevier/               # 📌 未来扩展
│   └── acm/                    # 📌 未来扩展
├── .gitignore                  # LaTeX 编译产物忽略规则
├── LICENSE                     # MIT License
└── README.md                   # 本文件
```

---

## 🚀 快速开始

### 编译模板

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

### 切换文档模式

`PaperTemplate.tex` 顶部提供了三种 IEEEtran 模式：

```latex
%\documentclass[conference]{IEEEtran}           % IEEE 会议版本
\documentclass[journal]{IEEEtran}               %% IEEE 期刊双栏版本（默认）
%\documentclass[12pt, draftclsnofoot, onecolumn]{IEEEtran}  % 期刊单栏版本
```

取消对应行的注释即可切换。

---

## 📚 参考文献库 (`mybib.bib`)

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

## 📦 已加载的 LaTeX 包

模板预载了以下常用包，覆盖论文写作的主要需求：

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

## 🎯 兼容期刊

本模板基于 **IEEEtran** 文档类，支持 **全部 IEEE 期刊与会议** 的投稿格式。切换 `journal`/`conference` 模式即可适配。以下是各领域的代表性期刊：

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

### 导师

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
