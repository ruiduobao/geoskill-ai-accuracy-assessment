# AI Model Accuracy Assessment (geoskill-ai-accuracy-assessment)

> Confusion matrix + OA/mIoU/F1 computation + spatial accuracy map, producing an accuracy assessment report (offline numpy equivalent implementation)

---

## 1. Overview

Performs a comprehensive accuracy assessment of classification/segmentation model predictions: confusion matrix, overall accuracy (OA), per-class Precision/Recall/F1, mean Intersection over Union (mIoU), Cohen's Kappa, and a local accuracy map revealing the spatial distribution of errors. This skill is an **offline numpy equivalent implementation** of a model evaluation pipeline: all metrics are computed directly with numpy, and every metric has unit tests against hand-computed references (per-cell confusion matrix, exact OA/mIoU/Kappa values, spatial localization of error blocks).

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-ai-accuracy-assessment.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `accuracy_report.json` | JSON | Confusion matrix/OA/mIoU/Kappa/per-class metrics |
| `spatial_accuracy.tif` | GeoTIFF | Local window accuracy map [0,1] |
| `output-manifest.json` | JSON | Run manifest (input/output/QA/exit code) |


## 6. Technical Principle

(see SKILL.md for details)

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
