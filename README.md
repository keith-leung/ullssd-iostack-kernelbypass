# A Systematic Literature Review of I/O Stack Evolution for Fully Utilizing SSDs

**Dawen Liang** and **Hengbo Cai** College of Engineering and Computer Science, Syracuse University

[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.18636357-blue.svg)](https://doi.org/10.5281/zenodo.18636357)
[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

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
├── data/                 # Raw data for tracking (3,131 records)
├── paper/
│   ├── main.tex          # Complete manuscript (IEEEtran conference style)
│   ├── refs.bib          # Bibliography (54 entries)
│   └── figures/          # TikZ-generated + image figures
├── protocol/
│   └── SLR_Protocol_v1.md  # Locked search protocol
└── Paper_Final.pdf

```

## Taxonomy

The review organizes I/O stack optimizations into three architectural paths:

| Path | Key Systems | Approach |
|------|-------------|----------|
| **Kernel Path** | blk-mq, blk-switch, D2FQ, io\_uring, Async I/O Stack, HORAE | Optimize within the existing Linux I/O stack |
| **Hybrid** | XRP (eBPF), I/O Passthru, RFUSE | Selectively bypass specific kernel layers |
| **Full Bypass** | SPDK, uFS, BypassD, Sandman, Aeolia | Remove the kernel entirely from the data path |

## Citation

```bibtex
@article{liang2026iostack,
  title={A Systematic Literature Review of {I/O} Stack Evolution for Fully Utilizing {SSDs}},
  author={Liang, Dawen and Cai, Hengbo},
  year={2026},
  publisher={Zenodo},
  howpublished={\url{[https://doi.org/10.5281/zenodo.18636357](https://doi.org/10.5281/zenodo.18636357)}},
  note={GitHub Repository: \url{[https://github.com/keith-leung/ullssd-iostack-kernelbypass](https://github.com/keith-leung/ullssd-iostack-kernelbypass)}}
}

```

## License

This work is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

