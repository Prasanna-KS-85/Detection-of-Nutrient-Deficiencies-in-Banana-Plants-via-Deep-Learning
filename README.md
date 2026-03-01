

# Detection of Nutrient Deficiencies in Banana Plants via Deep Learning

## Project Overview
This repository implements a deep learning methodology for identifying nutrient deficiencies in banana leaves through image classification. Several pre-trained Convolutional Neural Network (CNN) models were fine-tuned and assessed, with an ensemble method utilized to boost reliability and generalization against real-world farming challenges like inconsistent lighting, background clutter, and variable image resolution.

The application categorizes leaf images into nine distinct classes, covering eight deficiency types and a healthy control, while offering clear outputs such as symptom details and remedial measures.

---

## Objectives
- Identify nutrient shortfalls from banana leaf imagery
- Enhance model robustness through ensemble prediction techniques
- Manage variability typical in field-captured photos
- Deliver practical agricultural advice alongside classification results

---

## Models Used
We utilized and fine-tuned the following pre-trained CNN architectures using TensorFlow and Keras:

- MobileNetV2
- ResNet50V2
- InceptionV3

Each architecture was trained individually before being integrated into the final ensemble prediction pipeline.

---

## Dataset
- **Dataset Title:** Images of Nutrient Deficient Banana Plant Leaves
- **Image Count:** 7,000+
- **Class Categories:** 9
  - Boron deficiency
  - Calcium deficiency
  - Iron deficiency
  - Magnesium deficiency
  - Manganese deficiency
  - Potassium deficiency
  - Sulphur deficiency
  - Zinc deficiency
  - Healthy

**Source Reference:**
https://www.sciencedirect.com/science/article/pii/S2352340923002743

---

## Data Preprocessing
The training notebook incorporates the following preprocessing steps:

- Partitioning data into training, validation, and testing subsets
- Identifying and filtering out corrupted image files
- Standardizing image formats (converted to JPG)
- Resizing images according to model-specific requirements
- Applying normalization and architecture-specific preprocessing functions
- Implementing data augmentation methods like rotation, shifts, zoom, and horizontal flips

These measures ensure high-quality and consistent inputs for all models.

---

## Model Training
- **Platform:** TensorFlow / Keras
- **Loss Metric:** Categorical Cross-Entropy
- **Optimization Algorithm:** Adam
- **Primary Metric:** Accuracy
- **Approach:** Transfer learning with frozen base layers
- **Callbacks Implemented:**
  - Early Stopping
  - Reduce Learning Rate on Plateau

Models were trained independently, with weights saved in `.h5` format for inference and ensemble integration.

---

## Model Performance

**Table 1: Evaluation Metrics for Individual Models**

| Model        | Training Accuracy | Training Loss | Validation Accuracy | Validation Loss |
|-------------|------------------|---------------|---------------------|-----------------|
| ResNet50V2  | 80.07%           | 0.5525        | 66.70%              | 1.0832          |
| MobileNetV2 | 79.71%           | 0.5571        | 75.13%              | 0.7942          |
| InceptionV3 | 70.90%           | 0.8016        | 68.83%              | 0.8697          |

Among the single models, MobileNetV2 recorded the top validation accuracy. The ensemble method subsequently enhanced stability and performance on unseen test data.

---

## Ensemble Learning Strategy
To optimize performance in practical scenarios, we aggregated outputs from various CNN models via a weighted averaging technique:

Final Prediction = 0.4 × MobileNetV2 + 0.3 × ResNet50V2 + 0.3 × InceptionV3


This combination mitigates individual model bias, strengthens generalization, and ensures greater resilience under diverse field conditions.

---

## Inference and Decision Support
Upon processing a banana leaf image, the system outputs:
- The identified deficiency (or healthy status)
- Prediction confidence level
- Visual symptom breakdown
- Suggested remedies, including fertilizer and soil treatment advice

This functionality elevates the tool beyond simple classification, serving as a practical decision-support system for precision farming.

---

## User Interface
A user-friendly interface built with Gradio enables users to:
- Submit leaf images for analysis
- Obtain prediction results instantly
- Interactively review symptoms and corrective steps

---

## Technology Stack
- **Language:** Python
- **Frameworks:** TensorFlow, Keras
- **Architectures:** MobileNetV2, ResNet50V2, InceptionV3
- **Libraries:** NumPy, PIL, Matplotlib, Scikit-learn
- **Interface:** Gradio

---

## Important Note
**Please note: The notebooks included cannot be run immediately without modification.**
Users must manually configure dataset directories, model paths, and specific environment variables to match their local setup prior to training or running inference.