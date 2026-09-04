# Steel Surface Defect Detection Using YOLOv8

An AI-based computer vision system for automatic detection and
localization of surface defects in steel images using **YOLOv8** and
**Streamlit**.

## Project Overview

This project was developed during an **Arbotrix internship** in the
domain of Machine Learning and Reinforcement Learning. The system
automates steel surface inspection by detecting defects in uploaded
images and displaying their locations, classes, and confidence scores.

The trained YOLOv8-Nano model is integrated into a Streamlit web
application, providing an interactive inspection dashboard for users.

## Defect Classes

The model detects six types of steel surface defects:

1.  Crazing
2.  Inclusion
3.  Patches
4.  Pitted Surface
5.  Rolled-in Scale
6.  Scratches

## Key Features

-   Automatic steel surface defect detection
-   Detection of multiple defects in a single image
-   Bounding-box localization of defects
-   Confidence score for each detection
-   Adjustable confidence threshold
-   Original vs. detected image comparison
-   Inspection summary
-   Detection details table
-   Defect distribution chart
-   Interactive Streamlit interface

## System Workflow

``` text
Steel Surface Image
        ↓
Image Upload
        ↓
Streamlit Application
        ↓
YOLOv8-Nano Model (best.pt)
        ↓
Defect Detection
        ↓
Bounding Box + Class + Confidence
        ↓
Inspection Summary & Visual Results
```

## Dataset

The project uses a steel-surface defect dataset based on the **NEU
surface-defect category set**. The dataset was obtained from a public
GitHub repository and prepared for YOLO training.

### Dataset Statistics

-   Training images: **1,440**
-   Validation images: **360**
-   Number of classes: **6**

The original Pascal-VOC/XML annotations were converted into
YOLO-compatible `.txt` label files.

### YOLO Dataset Structure

``` text
steel_yolo/
├── images/
│   ├── train/
│   └── val/
├── labels/
│   ├── train/
│   └── val/
└── data.yaml
```

## Annotation Conversion

The original annotations were provided in Pascal-VOC XML format:

``` text
xmin, ymin, xmax, ymax
```

They were converted into the YOLO format:

``` text
class_id x_center y_center width height
```

Coordinates and bounding-box dimensions were normalized according to the
image width and height.

## Model

The project uses **YOLOv8-Nano (YOLOv8n)** from Ultralytics.

The model started from a **COCO-pretrained YOLOv8n checkpoint** and was
fine-tuned using transfer learning for steel surface defect detection.

### Training Configuration

  Parameter    Value
  ------------ -----------------------
  Model        YOLOv8n
  Image Size   640 × 640
  Batch Size   16
  Epochs       30
  Classes      6
  GPU          NVIDIA Tesla T4
  Framework    Ultralytics / PyTorch

The best-performing model weights were saved as:

``` text
best.pt
```

## Evaluation Results

The model was evaluated on **360 validation images containing 854
labeled defect instances**.

  Metric        Result
  ----------- --------
  Precision      0.722
  Recall         0.661
  mAP@50         0.736
  mAP@50-95      0.390

The model achieved an overall **mAP@50 of approximately 0.74**.

### Class-wise Performance

  Defect              Precision   Recall   mAP@50   mAP@50-95
  ----------------- ----------- -------- -------- -----------
  Crazing                 0.705    0.324    0.518       0.209
  Inclusion               0.734    0.748    0.816       0.477
  Patches                 0.789    0.873    0.927       0.597
  Pitted Surface          0.874    0.690    0.800       0.403
  Rolled-in Scale         0.505    0.492    0.511       0.228
  Scratches               0.723    0.841    0.841       0.424

## Streamlit Application

The trained `best.pt` model is integrated into a Streamlit application.

The application allows users to:

1.  Upload a steel-surface image in JPG, JPEG, or PNG format.
2.  Adjust the detection confidence threshold.
3.  Run AI-based defect detection.
4.  View the original and annotated images side by side.
5.  See bounding boxes, defect classes, and confidence scores.
6.  View an inspection summary.
7.  View detected defects in a results table.
8.  View a defect-distribution chart.

## Project Structure

A typical project structure is:

``` text
surface_defect_detection_steel/
├── best.pt
├── app.py
├── requirements.txt
├── README.md
└── ...
```

The exact structure may vary depending on the final project files
uploaded to the repository.

## Installation

### 1. Clone the Repository

``` bash
git clone https://github.com/kashaffnoor/surface_defect_detection_steel.git
cd surface_defect_detection_steel
```

### 2. Install Dependencies

``` bash
pip install -r requirements.txt
```

If a `requirements.txt` file is not included, the main libraries used by
the project include:

``` text
ultralytics
streamlit
torch
opencv-python
Pillow
pandas
albumentations
```

## Run the Streamlit Application

Run:

``` bash
streamlit run app.py
```

Then open the local Streamlit URL shown in the terminal, usually:

``` text
http://localhost:8501
```

## Google Colab Training

Model training was performed in **Google Colab using a GPU runtime**.

The general training pipeline was:

``` text
Dataset Acquisition
        ↓
XML Annotation Conversion
        ↓
YOLO Dataset Preparation
        ↓
data.yaml Configuration
        ↓
YOLOv8n Training
        ↓
Validation
        ↓
best.pt
        ↓
Streamlit Integration
```

## Confidence Threshold

The application provides an adjustable confidence threshold.

For example, a threshold of `0.50` means detections below 50% confidence
are filtered out.

-   **Higher threshold:** fewer false detections, but some genuine
    defects may be missed.
-   **Lower threshold:** more possible defects are shown, but false
    positives may increase.

## Technologies Used

-   **Python**
-   **YOLOv8 / Ultralytics**
-   **PyTorch**
-   **OpenCV**
-   **Pillow**
-   **Albumentations**
-   **Pandas**
-   **Streamlit**
-   **Google Colab**
-   **Google Drive**
-   **GitHub**

## Limitations and Future Improvements

The current model demonstrates a complete end-to-end detection pipeline,
but further optimization can improve performance.

Potential improvements include:

-   Increasing the size and diversity of the training dataset
-   Additional data augmentation
-   Hyperparameter optimization
-   Improving performance on the **Rolled-in Scale** class
-   Improving the stricter mAP@50-95 metric
-   Testing additional YOLO model variants
-   Deploying the application on a cloud platform
-   Optimizing inference for real-time industrial inspection

The current model should be considered a demonstration/prototype rather
than a fully autonomous industrial inspection system.

## Conclusion

This project demonstrates a complete AI-based steel surface inspection
pipeline, from dataset preparation and annotation conversion to YOLOv8
training, evaluation, and Streamlit deployment.

The system can detect six categories of steel surface defects and
provide their locations and confidence scores through an interactive web
interface.

## References

1.  Ultralytics YOLOv8 Documentation
2.  NEU Surface Defect Database
3.  Kshitij0605/Steel-Defect-Detection-using-Yolo-models --- dataset
    repository
4.  Python Documentation
5.  Streamlit Documentation
6.  PyTorch Documentation

## Internship

**Organization:** Arbotrix\
**Domain:** Machine Learning and Reinforcement Learning\
**Year:** 2026
