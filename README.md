# NYCU Computer Vision 2026 HW3

* **Student ID:** 314511037
* **Name:** 張周芳

## Introduction
This project implements an object detection pipeline for HW2 using a DETR-based architecture with a ResNet-50 backbone.  
The final model is based on Deformable DETR and is designed to improve detection performance on small RGB images.

The project includes:
- A notebook for training the detection model
- A notebook for inference on the test dataset
- Validation evaluation using COCO-format metrics
- Visualization utilities for prediction analysis

## Dataset
Place the dataset folder under the following structure:

```bash
CV_HW3/
├─ hw3-data-release/
│   ├── test_image_name_to_ids.json
│   ├── test_release
│   └── train
├─ checkpoints/
│   └─ best_ap50_maskrcnn.pth # test mAP model
├─ cv-hw3-data_analysis.ipynb
├─ cv-hw3-training.ipynb
├─ cv-hw3-inference.ipynb
├─ README.md
├─ test-results.json
└─ requirements.txt
```
> Note: he dataset and model files are not included in this repository.
> Please download or prepare the dataset according to the structure above (e.g., by extracting the provided assignment package).
> Both the best mAP models can be trained from scratch using the provided notebooks.
> If you want to skip training and run inference directly, you can download the best trained model from the cloud:    
> - **Best model:** [model path](https://drive.google.com/file/d/1a4ifemWZ1A1Z6jSpaC0_WIpTkJ-pTO4m/view?usp=sharing)
> - After downloading, place the checkpoint file at: `./checkpoints_deformable_detr/best_model_by_map.pth`

> On a **local machine**, place the dataset in the same structure and update notebook file paths to match your directories.

## Environment Setup

- Python 3.11+
- GPU recommended (CUDA supported)

This project was developed and tested on rtxgb10.

For running this project on your local machine, follow the steps below.

### Step 0: Clone the Repository

```bash
git clone https://github.com/fangfangirl/CV_HW2.git
cd CV_HW2
```
### Step1: Using Conda (Recommended do)

```bash
# Create a conda environment
conda create -n cv-hw2 python=3.11 -y

# Activate environment
conda activate cv-hw2
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

### Training

1. Open and run `cv-hw2-training.ipynb` to train the object detection model.
2. This notebook trains a Deformable DETR-based model with a ResNet-50 backbone on the training dataset.
3. During training, the model is evaluated on the validation dataset using COCO-format metrics.
4. The best checkpoint is saved based on validation performance (e.g., `best_model_by_map.pth`).

### Inference

- Open and run `cv-hw2-inference.ipynb` to generate predictions on the test dataset.
- If you want to skip training, you can directly use the pretrained best model checkpoint.
- Ensure the checkpoint file is placed in the directory specified in the notebook.
- Make sure the dataset path and checkpoint path are correctly updated before execution.

> Note: The trained checkpoint is required for inference.

## Performance Snapshot

The generated prediction file is stored in the cloud. You can download [`pred.json`](https://drive.google.com/file/d/1tNGEpXK-iZYgnHvPwtPL3892h5V3rmDD/view?usp=sharing) if needed.
The table below summarizes the model performance on the validation dataset.

| Model             | Backbone  | Validation mAP | Test mAP |
|------------------|-----------|----------------| ----------------|
| Deformable DETR  | ResNet-50 | 0.4768 | 0.38 |

### Leaderboard / Final Results

The screenshot below shows the final leaderboard / result for this project:

<img width="1735" height="70" alt="image" src="https://github.com/user-attachments/assets/5bc553a2-e282-4717-babc-9c1ae48781ea" />

![result.png](https://github.com/user-attachments/assets/164b7ff1-5433-4428-943a-99b36230a793)
