# Noise-Augmented Training of a Lightweight 1D CNN for Single-Lead ECG Classification Toward Wearable Deployment

Real-time multi-class ECG arrhythmia classification (NSR, AFIB, PVC, LBBB) pipeline featuring offline model training and embedded deployment on a Raspberry Pi system.

## Key Features

* **Multi-Database Training:** Uses MIT-BIH, PTB-XL, LTAFDB, and INCART datasets.
* **Patient-Wise Splits:** Record-level 75/12.5/12.5 train/val/test split.
* **Noise Augmentation:** Injects NSTDB noise (BW, EM, MA) at 5–10 dB SNR.
* **Dual-Input CNN:** Combines 1D residual CNN signal processing with RR-interval/QRS metrics.
* **Multi-Core Pipeline (`deploy_main.py`):** Multi-process deployment pinned across CPU cores:
  * Acquisition & Pico interfacing
  * Signal segmentation (1,024-sample windows)
  * Real-time IIR SOS filtering & normalization
  * Edge TFLite model inference
  * OLED status display

## Hardware & Components

* Raspberry Pi 4 B
* Raspberry Pi Pico (RP2040)
* AD8232 Heart Rate Monitor
* SSD1306 I2C OLED Display


## Requirements

```text
# Python Packages
wfdb
scipy
numpy<2.0
pandas==2.2.2
tensorflow
seaborn
matplotlib
scikit-learn

# Deployment / System
wiringpi
tflite-runtime
```

## Usage

### 1. Model Training
Run `data_preparation_augmentation_and_model_training.ipynb` to train the model and generate `model.tflite`.

### 2. Live Execution
Run the deployment pipeline on the Raspberry Pi:

```bash
cd deployment
python3 deploy_main.py
```

## Project Structure

```text
.
├── data_preparation_augmentation_and_model_training.ipynb
└── deployment/
    ├── deploy_acquisition.py
    ├── deploy_filtering.py
    ├── deploy_inference.py
    ├── deploy_main.py
    ├── deploy_oled.py
    ├── deploy_pico.py
    ├── deploy_segmentation.py
    └── model.tflite
```

## Contributors

* **Abdullah Dave Adjuran** - *Ateneo de Zamboanga University, Engineering Department*
* **Abdulaziz Abdukahil** - *Ateneo de Zamboanga University, Engineering Department*