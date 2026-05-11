# NYCU Computer Vision 2026 HW3

* **Student ID:** 314511037
* **Name:** 張周芳

## Introduction

This repository contains my implementation for NYCU Computer Vision 2026 HW3.

The task is instance segmentation on microscopic cell images.  
I use a Mask R-CNN model with a ResNet-50 FPN backbone from `torchvision.models.detection`.

The project includes:

- Data analysis notebook
- Training pipeline notebook
- Inference pipeline notebook
- COCO-style validation evaluation
- Test prediction generation
- Visualization utilities for checking masks and predictions

## Dataset
Place the dataset folder under the following structure:

```bash
CV_HW3/
├─ hw3-data-release/
│   ├── test_image_name_to_ids.json
│   ├── test_release
│   └── train
├─ checkpoints/
│   └─ best_ap50_maskrcnn.pth # test AP50 model
├─ cv-hw3-data_analysis.ipynb
├─ cv-hw3-training.ipynb
├─ cv-hw3-inference.ipynb
├─ README.md
├─ test-results.json
└─ requirements.txt
```

> Note: he dataset and model files are not included in this repository.
> Please download or prepare the dataset according to the structure above (e.g., by extracting the provided assignment package).
> The best AP50 models can be trained from scratch using the provided notebooks.
> If you want to skip training and run inference directly, you can download the best trained model from the cloud:    
> - **Best model:** [model path](https://drive.google.com/file/d/1P5X2FcFVxI3rROxeYrErHvfKLGVY72Kx/view?usp=sharing)
> - After downloading, place the checkpoint file at: `./checkpoints/best_ap50_maskrcnn.pth`

> On a **local machine**, place the dataset in the same structure and update notebook file paths to match your directories.

## Environment Setup

- Python 3.11+
- GPU recommended (CUDA supported)

This project was developed and tested on rtxgb10.

For running this project on your local machine, follow the steps below.

### Step 0: Clone the Repository

```bash
git clone https://github.com/fangfangirl/CV_HW3.git
cd CV_HW3
```
### Step1: Using Conda (Recommended do)

```bash
# Create a conda environment
conda create -n cv-hw3 python=3.11 -y

# Activate environment
conda activate cv-hw3
```
### Step2: Install PyTorch

Please install PyTorch based on your system configuration:

1. Visit: [https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/)
2. Select your OS, package (pip), and CUDA version
3. Run the generated command

Example (CUDA 12.6):
```bash
pip3 install torch torchvision --index-url https://download.pytorch.org/whl/cu126
```
### Step3: Install Other Dependencies
```bash
pip install -r requirements.txt
```

## Usage

### Data Analysis

1. Open and run `cv-hw3-data_analysis.ipynb` to check the dataset.
2. This notebook visualizes training images and masks.
3. It also provides basic information about the dataset, such as image and mask structure.
4. This step is optional and is mainly used for understanding the dataset.

### Training

1. Open and run `cv-hw3-training-pipeline_exp3.ipynb` to train the instance segmentation model.
2. This notebook trains a Mask R-CNN model with a ResNet-50 FPN backbone on the training dataset.
3. During training, the model is evaluated on the validation dataset.
4. The best checkpoint is saved based on validation performance.
5. The saved checkpoint is stored at `hw3/checkpoints/best_ap50_maskrcnn.pth`.

> Note: The training notebook may use `wandb` for logging.  
> If `wandb` asks for login, you can log in with your own account or disable it by adding:
>
> ```python
> import os
> os.environ["WANDB_MODE"] = "disabled"
> ```
>
> You can also comment out `wandb.login()` if it appears in the notebook.

### Inference

1. Open and run `cv-hw3-inference-pipeline.ipynb` to generate predictions on the test dataset.
2. The notebook loads the trained Mask R-CNN checkpoint.
3. Ensure the checkpoint file is placed in the directory specified in the notebook.
4. Make sure the dataset path and checkpoint path are correctly updated before execution.
5. The generated prediction file is saved as `hw3/test-results.json`.

> Note: The trained checkpoint is required for inference.
## Performance Snapshot

The generated prediction file is stored in the cloud. You can download [`pred.json`](https://drive.google.com/file/d/1tNGEpXK-iZYgnHvPwtPL3892h5V3rmDD/view?usp=sharing) if needed.
The table below summarizes the model performance on the validation dataset.

| Model             | Backbone  | Validation mAP | Test mAP |
|------------------|-----------|----------------| ----------------|
| Deformable DETR  | ResNet-50 |  | 0.5266 |

### Leaderboard / Final Results

The screenshot below shows the final leaderboard / result for this project:

<img width="1735" height="70" alt="image" src="https://github.com/user-attachments/assets/5bc553a2-e282-4717-babc-9c1ae48781ea" />
