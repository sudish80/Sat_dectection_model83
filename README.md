# EuroSAT Land-Cover Classification — ResNet-50 Fine-Tuning

Fine-tunes a **ResNet-50** (ImageNet-pretrained) on the **EuroSAT** satellite-imagery dataset for 10-class land-use / land-cover classification.

## Results

- **Best validation accuracy:** 99.11%
- **Training accuracy:** 99.80%
- **Training time:** ~58 min on Tesla T4 GPU

## Model

- Architecture: ResNet-50 with custom 10-class classification head (dropout + linear layers)
- Optimizer: AdamW with discriminative learning rates
- Scheduler: OneCycleLR
- Loss: CrossEntropyLoss with label smoothing (0.1)

## Dataset

EuroSAT contains **27,000 labeled 64×64 Sentinel-2 RGB image patches** across **10 classes**:

0. AnnualCrop
1. Forest
2. HerbaceousVegetation
3. Highway
4. Industrial
5. Pasture
6. PermanentCrop
7. Residential
8. River
9. SeaLake

## Usage

Open `EuroSAT_ResNet50_FineTuning.ipynb` in Google Colab with a GPU runtime and run all cells.

## Links

- **GitHub:** https://github.com/sudish80/Sat_dectection_model83
- **Hugging Face:** https://huggingface.co/buckets/sudish111/Sat_dectection_model83-bucket
