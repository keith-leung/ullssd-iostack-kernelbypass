# A Systematic Literature Review of I/O Stack Evolution for Fully Utilizing SSDs

**Dawen Liang** and **Hengbo Cai**  
College of Engineering and Computer Science, Syracuse University

[![arXiv](https://img.shields.io/badge/arXiv-XXXX.XXXXX-b31b1b.svg)](https://arxiv.org/abs/XXXX.XXXXX)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

> **Update the arXiv badge URL once the paper is posted.**

## Abstract

The rise of ultra-low latency (ULL) NVMe SSDs, with device access times nearing single-digit microseconds, has shifted the performance bottleneck from storage hardware to the software I/O stack. This systematic literature review examines how the I/O stack has evolved—from kernel-based mediation to hybrid and full kernel bypass solutions—to fully harness the capabilities of modern SSDs. Following **PRISMA 2020** guidelines, we gathered **3,131 records** from four databases and via citation-based snowballing, eventually including **398 studies** covering 2012–2025. We organize the reviewed work into a three-path taxonomy: **Kernel Path** optimizations (blk-mq, io\_uring, polling, file system adaptations), **Hybrid Approaches** (eBPF/XRP, NVMe I/O Passthrough, modernized FUSE), and **Full Kernel Bypass** solutions (SPDK, user-space file systems, interrupt-based user-space stacks). **44 papers** are deeply analyzed, with **189 citable studies** (QA ≥ 1) informing the technical synthesis.

## Key Findings

- The Linux kernel storage path contributes **up to 50%** of end-to-end I/O latency on modern NVMe devices
- Kernel-path optimizations like blk-switch achieve up to **130× average latency improvement** over standard Linux
- Hybrid approaches (XRP, I/O Passthru) deliver **30–94% throughput gains** while preserving kernel safety
- Full bypass is evolving beyond SPDK's polling model toward **energy-efficient** (Sandman) and **interrupt-based** (Aeolia) designs
- The boundaries between kernel and bypass are **converging** through eBPF programmability and NVMe passthrough

## PRISMA Flow

```
Records identified (n = 3,131)
  ├── Database searches DB1–DB5 (n = 3,051)
  └── Prior review work (n = 80)
         │
  Duplicates removed (n = 710)
         │
  Stage 1: Title & abstract screening (n = 2,341)
  │     Excluded (n = 1,849)
  │
  Stage 2: Full-text eligibility (n = 572)
  │     Excluded (n = 174)
  │
  Studies included (n = 398)
  ├── QA ≥ 1 citable (n = 189)
  └── QA = 0 audit-only (n = 209)

Checksum: 398 + 174 + 1,849 + 710 = 3,131 ✓
```

## Repository Structure

```
ullssd-iostack-kernelbypass/
├── README.md
├── LICENSE
├── data/                 # Raw data for tracking
├── paper/
│   ├── main.tex          # Complete manuscript (IEEEtran conference style)
│   ├── refs.bib          # Bibliography (54 entries)
│   └── figures/          # TikZ-generated + image figures
│       └── fig_*.png
├── protocol/
│   └── SLR_Protocol_v1.md  # Locked search protocol (queries, EC criteria, databases)
└── Paper_Final.pdf
```

## Taxonomy

The review organizes I/O stack optimizations into three architectural paths:

| Path | Key Systems | Approach |
|------|-------------|----------|
| **Kernel Path** | blk-mq, blk-switch, D2FQ, io\_uring, Async I/O Stack, HORAE | Optimize within the existing Linux I/O stack |
| **Hybrid** | XRP (eBPF), I/O Passthru, RFUSE | Selectively bypass specific kernel layers |
| **Full Bypass** | SPDK, uFS, BypassD, Sandman, Aeolia | Remove the kernel entirely from the data path |

## Search Strategy

- **Databases**: Google Scholar (DB1), ACM Digital Library (DB2), IEEE Xplore (DB3), Semantic Scholar API (DB4), Forward/backward snowballing (DB5)
- **Time range**: 2012 – May 31, 2025
- **5 query strings** covering io\_uring, SPDK, blk-mq, kernel bypass, eBPF, ultra-low latency SSD, and user-space NVMe drivers
- **Exclusion criteria** (EC1 > EC2 > EC3 > EC4 > EC5): Non-CS, pure hardware, out-of-scope (CXL/ZNS-only/KV-SSD/computational storage), non-peer-reviewed, duplicate contribution

## How to Compile

```bash
# Requires a LaTeX distribution with IEEEtran class
cd paper/
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

## Citation

```bibtex
@article{liang2026iostack,
  title={A Systematic Literature Review of {I/O} Stack Evolution for Fully Utilizing {SSDs}},
  author={Liang, Dawen and Cai, Hengbo},
  journal={arXiv preprint arXiv:XXXX.XXXXX},
  year={2026}
}
```

## License

This work is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You are free to share and adapt this material with appropriate attribution.
