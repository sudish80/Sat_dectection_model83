---
license: mit
---

# EuroSAT Land-Cover Classification — ResNet-50 Fine-Tuning

Fine-tunes a **ResNet-50** (ImageNet-pretrained) on the **EuroSAT** satellite-imagery dataset for 10-class land-use / land-cover classification.

## Results

| Metric | Value |
|--------|-------|
| Best validation accuracy | **99.11%** |
| Training accuracy (final) | **99.80%** |
| Training time | ~58 min on Tesla T4 GPU |
| Total parameters | 24,562,250 |

## Visualizations

These plots are generated automatically when the notebook runs:

![Training Curves](training_curves.png)
*Loss & accuracy curves over 15 epochs*

![Confusion Matrix](confusion_matrix.png)
*Normalized confusion matrix on the test set*

![Per-Class Accuracy](per_class_accuracy.png)
*Accuracy breakdown per land-cover class*

![Grad-CAM Explainability](gradcam.png)
*Grad-CAM heatmaps showing what the model focuses on*

## Dataset

EuroSAT contains **27,000 labeled 64×64 Sentinel-2 RGB image patches** across **10 classes**:

| Class | Label | Description |
|-------|-------|-------------|
| AnnualCrop | 0 | Crops that are replanted yearly |
| Forest | 1 | Dense tree cover |
| HerbaceousVegetation | 2 | Grasslands, shrubs |
| Highway | 3 | Roads and highways |
| Industrial | 4 | Industrial buildings/factories |
| Pasture | 5 | Grazing land |
| PermanentCrop | 6 | Vineyards, orchards |
| Residential | 7 | Houses, buildings |
| River | 8 | Rivers, water bodies |
| SeaLake | 9 | Lakes, sea |

## Model Architecture

```
ResNet-50 (ImageNet pretrained)
  ├── Conv1 → BatchNorm → ReLU → MaxPool
  ├── Layer1 (3 bottleneck blocks)
  ├── Layer2 (4 bottleneck blocks)
  ├── Layer3 (6 bottleneck blocks)
  ├── Layer4 (3 bottleneck blocks)
  ├── Global Average Pooling
  └── Custom Head:
       ├── Dropout(0.3)
       ├── Linear(2048 → 512) → ReLU
       ├── Dropout(0.2)
       └── Linear(512 → 10)
```

## Training Details

- **Optimizer:** AdamW (discriminative LR: 1e-4 backbone, 1e-3 head)
- **Scheduler:** OneCycleLR
- **Loss:** CrossEntropyLoss with label smoothing (0.1)
- **Batch size:** 64
- **Epochs:** 15
- **Augmentation:** Random flips, ±15° rotation, ColorJitter

## Usage

Open `EuroSAT_ResNet50_FineTuning.ipynb` in Google Colab with a **GPU runtime** and run all cells.

### Requirements

- Python 3.10+, PyTorch, torchvision, datasets, matplotlib, seaborn, scikit-learn, PIL, kagglehub

## Model Weights

`resnet50_eurosat_finetuned.pth` (~98.6 MB) — available in this repo.

## Links

- **GitHub:** https://github.com/sudish80/Sat_dectection_model83
- **Hugging Face:** https://huggingface.co/buckets/sudish111/Sat_dectection_model83-bucket
