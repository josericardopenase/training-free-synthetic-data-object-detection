# Controllable Synthetic Data for Data-Efficient Object Detection

**Training-free** pipeline that turns structured text prompts into pseudo-labeled object-detection datasets — then uses them to train detectors when real annotations are scarce or expensive.

**Project page:** [josericardopenase.github.io/training-free-synthetic-data-object-detection](https://josericardopenase.github.io/training-free-synthetic-data-object-detection/)

> Preprint submitted to *Image and Vision Computing* (2026). PDF will be linked here after the arXiv upload.

## Authors

Jose R. Peña-Seco<sup>1</sup>, Jonay Suárez-Ramírez<sup>2</sup>, Adrian Penate-Sanchez<sup>1</sup>, Nelson Monzón<sup>1</sup>

<sup>1</sup> University of Las Palmas de Gran Canaria (ULPGC) · <sup>2</sup> Qualitas Artificial Intelligence and Science (QAISC)

## Overview

Collecting instance-level boxes for real-world detection is costly, especially under rare weather, viewpoints, or object counts. This repository implements a fully automatic augmentation pipeline:

1. **Structured prompts** — an LLM (Mistral-7B-Instruct) expands a Cartesian product of class, environment, weather, and object quantity into natural-language captions.
2. **Image synthesis** — FLUX generates images from those prompts (no generator fine-tuning).
3. **Pseudo-labeling** — Grounded SAM produces boxes with a **one-category-per-image** strategy to cut false positives and handle domain-specific class names.
4. **Detector training** — YOLO26 / RT-DETR train on mixtures of real and synthetic data, from scratch.

Domain diagnostics (CLIP embeddings + t-SNE + neighborhood metrics) help explain when the synthetic set helps and when it does not.

## Highlights

| Setting | Result |
|--------|--------|
| PASCAL VOC, full real data + 16k synth | up to **+9.0 pp AP50** (YOLO26-n) |
| PASCAL VOC, 1k real + 16k synth | up to **+35.4 pp AP50** |
| Vessels & Boats (industrial maritime) | ~⅓ of real images + synth **matches full-real AP** |
| Cross-domain | Strong gains on diverse / maritime domains; limited transfer on viewpoint-locked KITTI |

Evaluated on six benchmarks: PASCAL VOC 2012, MS-COCO subset, KITTI, African Wildlife, Home Objects 3K, and Vessels & Boats.

## Repository layout

```text
docs/                 Project page (GitHub Pages)
training_scripts/     Detector training entry points
*.ipynb               Prompting, FLUX generation, Grounded SAM labeling, domain-shift analysis
training_history/     Experiment logs and curves
requirements.txt      Python dependencies
```

## Quick start

```bash
# Environment (uv or pip)
uv sync
# or: pip install -r requirements.txt

# Typical workflow (notebooks)
# 1) prompt_generation.ipynb
# 2) diffusion_generation.ipynb
# 3) groundedsam_labeling.ipynb
# 4) training_scripts/ + yolo_training.ipynb
```

Preview the project page locally:

```bash
cd docs && python3 -m http.server 8000
# http://localhost:8000
```

## Citation

```bibtex
@article{penaseco2026controllable,
  title={Controllable Synthetic Data Generation for Data-Efficient Object Detection in Real-World Domains},
  author={Pe{\~n}a-Seco, Jose R. and Su{\'a}rez-Ram{\'i}rez, Jonay and Penate-Sanchez, Adrian and Monz{\'o}n, Nelson},
  journal={Image and Vision Computing (preprint)},
  year={2026}
}
```

## Acknowledgments

Supported by the Cabildo de Gran Canaria (Resolution 45/2021) and QAISC. The Vessels & Boats dataset was provided by QAISC under research contract C2024/54 with ULPGC.
