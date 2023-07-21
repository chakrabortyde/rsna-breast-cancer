# Screening Mammography Breast Cancer Detection

## Abstract

The goal of this project is to develop a machine-learning model to identify breast cancer in mammograms obtained from regular screening exams. The dataset consists of radiographic breast images of approximately 20,000 female subjects, along with metadata such as patient age, breast density, whether the breast was positive for malignant cancer, and further follow-up information. The model will be trained on the provided training set and evaluated on a hidden test set, with the ultimate goal of improving the accuracy and efficiency of breast cancer detection, reducing costs and unnecessary medical procedures, and extending the benefits of early detection to a broader population. The current state-of-the-art probabilistic F1 score (pF1) stands at 55%.

## Introduction

Breast cancer is the most commonly occurring cancer worldwide and early detection is critical in reducing mortality rates. However, current screening programs are expensive, require the expertise of highly-trained radiologists, and often result in false positives, leading to unnecessary medical procedures and increased patient anxiety. By developing a machine learning model, we aim to improve the accuracy, efficiency, and accessibility of breast cancer screening programs. This would have significant implications for patient and health care delivery, reducing costs and unnecessary medical procedures, and extending the benefits of early detection to a broader population. Application of this technology could be used in clinical settings to assist radiologists in the screening process, reducing their workload and improving the accuracy of their diagnosis. This could also be used in areas with limited access to radiologists, where the machine learning model could provide a preliminary diagnosis before being reviewed by a radiologist. Ultimately, this technology could help save lives by improving the early detection and treatment of breast cancer.

## Proposal

### Approach

Based on the context provided and the description statement, this is a binary classification problem, where the goal is to classify mammogram images into positive/negative. We aim to train a model based on not only the target variable but also additional metadata as described in the dataset. We later plan to drop some of these parameters as few of them are not present in the test data set, hoping that the model has extracted enough useful information from them to help reduce false positives.

### Dataset

This dataset comes from the Kaggle challenge **"RSNA Screening Mammography Breast Cancer Detection"** by the Radiological Society of North America. It contains radiographic breast images of roughly 20,000 female patients (60:40 split) with usually 4 images per patient (2 lateral \[`left`, `right`\] per view \[`mediolateral-oblique`, `crainal-caudal`\]).
1. `site id`, `machine id` - ID code for the source hospital, imaging device
2. `patient id`, `image id` - ID code for the patient and respective image
3. `laterality` - whether the image is of the left or right breast
4. `view` - orientation of the image
5. `age` - patient’s age in years
6. `implant` - whether the patient had breast implants at the patient level
7. `density` **(train only)** - rating for how dense the breast tissue is, with A being the least dense and D being the most dense
8. `biopsy` **(train only)** - whether a follow-up biopsy was performed on the breast
9. `invasive` **(train only)** - whether or not cancer (if `true`) proved to be invasive
10. `BIRADS` **(train only)** - `0` if the breast required follow-up, `1` if the breast was rated as negative for cancer, and `2` if the breast was rated as normal
11. `difficult negative case` **(train only)** - `true` if the case was unusually difficult
12. `cancer` **(target)** - whether or not the breast was positive for malignant cancer

### Feature extraction

The feature vectors for the images are not provided in the dataset and will need to be extracted using an encoder module. The images may also be subjected to context-based cropping and blurring. No other pre-processing requirement is estimated, but this need may be modified in the future. We plan to train the secondary network on all the five image properties, and later remove everything except the target variable.

![Representation of the feature extraction and secondary network training flow.](/img/proposed-network.png)

## References

- National Cancer Institute. Common Cancer Types. https://www.cancer.gov/types/common-cancers, 2022.
- Radiological Society of North America. RSNA Screening Mammography Breast Cancer Detection. https://www.kaggle.com/competitions/rsna-breast-cancer-detection/leaderboard, 2023.
