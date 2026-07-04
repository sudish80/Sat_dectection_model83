---
license: mit
---

# EuroSAT Land-Cover Classification — ResNet-50 Fine-Tuning

Fine-tunes a **ResNet-50** (ImageNet-pretrained) on the **EuroSAT** satellite-imagery dataset for 10-class land-use / land-cover classification.

## Results

| Metric | Value |
|--------|-------|
| Best validation accuracy | **99.11%** |
| Training accuracy | **99.80%** |
| Training time | ~58 min on Tesla T4 GPU |

## Model Architecture

- **Backbone:** ResNet-50 (ImageNet-pretrained)
- **Head:** `Dropout(0.3) → Linear(2048→512) → ReLU → Dropout(0.2) → Linear(512→10)`
- **Optimizer:** AdamW with discriminative learning rates (backbone: 1e-4, head: 1e-3)
- **Scheduler:** OneCycleLR
- **Loss:** CrossEntropyLoss with label smoothing (0.1)

## Dataset

EuroSAT contains **27,000 labeled 64×64 Sentinel-2 RGB image patches** across **10 classes**:

| Class | Label |
|-------|-------|
| AnnualCrop | 0 |
| Forest | 1 |
| HerbaceousVegetation | 2 |
| Highway | 3 |
| Industrial | 4 |
| Pasture | 5 |
| PermanentCrop | 6 |
| Residential | 7 |
| River | 8 |
| SeaLake | 9 |

## Usage

Open `EuroSAT_ResNet50_FineTuning.ipynb` in Google Colab with a **GPU runtime** (T4 or better) and run all cells.

### Requirements
- Python 3.10+
- PyTorch, torchvision, datasets, matplotlib, seaborn, scikit-learn, PIL, kagglehub

## Links

- **GitHub:** https://github.com/sudish80/Sat_dectection_model83
- **Hugging Face:** https://huggingface.co/buckets/sudish111/Sat_dectection_model83-bucket
