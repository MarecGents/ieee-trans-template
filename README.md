# IEEE Trans Template

> A LaTeX Template for IEEE Transactions

一篇开箱即用的 IEEE 期刊论文 LaTeX 模板，适合作为通信、信号处理、计算机等工程领域论文写作的起点。

---

## 📁 目录结构

```
ieee-trans-template/
├── templates/                  # 论文模板目录（可扩展其他期刊）
│   ├── PaperTemplate.tex       # 主模板文件 (IEEEtran, journal 双栏)
│   ├── mybib.bib               # 参考文献库（预置 30+ IEEE 期刊缩写）
│   ├── citesort.sty            # 引用排序与压缩样式
│   ├── figure/                 # 图片资源目录
│   └── pdf/                    # PDF 输出目录
├── .gitignore                  # LaTeX 编译产物忽略规则
├── LICENSE                     # MIT License
└── README.md                   # 本文件
```

> 💡 **未来扩展**：如需添加其他期刊模板（如 Elsevier、ACM、Springer 等），可在 `templates/` 下按期刊名创建子目录，例如 `templates/elsevier/`、`templates/acm/`。

---

## 🚀 快速开始

### 编译模板

使用标准的 `pdflatex` + `bibtex` 编译流程：

```bash
# 1. 进入模板目录
cd templates

# 2. 编译主文档（需 2-3 次以解析交叉引用）
pdflatex PaperTemplate.tex
bibtex PaperTemplate
pdflatex PaperTemplate.tex
pdflatex PaperTemplate.tex
```

或使用 `latexmk` 一键编译（推荐）：

```bash
cd templates
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

## 📄 许可证

[MIT License](LICENSE) © 2026 MarecGents
