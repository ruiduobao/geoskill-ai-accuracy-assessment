---
name: geoskill-ai-accuracy-assessment
description: '混淆矩阵+OA/mIoU/F1计算+空间精度图，输出精度评估报告（离线numpy等价实现）'
---

# AI模型精度评估 | AI Model Accuracy Assessment

Performs a comprehensive accuracy assessment of classification/segmentation model predictions: confusion matrix, overall accuracy (OA), per-class Precision/Recall/F1, mean Intersection over Union (mIoU), Cohen's Kappa, and local accuracy maps that reveal the spatial distribution of errors.

This skill is an **offline NumPy-equivalent implementation** of the model evaluation pipeline: all metrics are computed directly with NumPy, and each one has unit tests against hand-computed baselines (cell-by-cell confusion matrix, exact OA/mIoU/Kappa values, spatial localization of error blocks).

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy scikit-learn geopandas shapely
```

## Usage / 使用方法

### Example 1 (Synthetic Data, Offline)

```bash
python geoskill-ai-accuracy-assessment.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 2: Synthetic Evaluation Experiment (Offline, with Known Error Blocks)

```bash
python geoskill-ai-accuracy-assessment.py --bbox 116.0 39.0 117.0 40.0 --synthetic --window 7 --output-dir ./out
```

### Example 3: Prediction + Ground Truth Dual Rasters

```bash
python geoskill-ai-accuracy-assessment.py --input pred.tif --truth ref.tif --output-dir ./out
```

### 示例 4：单文件双波段 [pred, truth]

```bash
python geoskill-ai-accuracy-assessment.py --input pair.tif --window 9 --output-dir ./out
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `accuracy_report.json` | JSON | Confusion matrix/OA/mIoU/Kappa/per-class metrics |
| `spatial_accuracy.tif` | GeoTIFF | Windowed local accuracy map [0,1] |
| `output-manifest.json` | JSON | Run manifest (inputs/outputs/QA/exit code) |

## Data Source / 数据源 / Source

Prediction/truth label rasters, or --synthetic (truth stripes + systematic error blocks + randomly scattered errors).

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is done locally; no user data is ever uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
