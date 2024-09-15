# Image Feature Extraction

## Problem Statement

The objective of this project is to create a machine learning model that extracts entity values from images, such as weight, volume, dimensions, and more. This solution is particularly useful in fields like healthcare, e-commerce, and content moderation, where obtaining detailed product information from images is essential.

The dataset contains product images and corresponding entity values such as weight or volume, and the goal is to predict the entity value from the image. 

## Dataset Description

### Columns:
- **index**: A unique identifier for the data sample.
- **image_link**: A URL where the product image is available for download.
- **group_id**: Category code of the product.
- **entity_name**: The name of the entity (e.g., `item_weight`, `item_volume`).
- **entity_value**: The corresponding value of the entity (e.g., `34 gram`).

### Dataset Files:
- `dataset/train.csv`: Contains training data with entity values.
- `dataset/test.csv`: Test data without the target entity values.
- `dataset/sample_test.csv`: A sample test file for reference.
- `dataset/sample_test_out.csv`: A sample output file for reference.

### Source Files:
- **src/sanity.py**: A sanity checker script to validate your output file's format.
- **src/utils.py**: Contains helper functions for downloading images from the provided URLs.
- **src/constants.py**: Includes the allowed units for each entity type.
- **sample_code.py**: A sample code file to help generate an output file in the required format.

## Goal

For the test set, the goal is to predict the `entity_value` for each image and return the results in a specific format: 
- **Format**: `x unit`, where `x` is a float and `unit` is a valid unit as defined in `constants.py`.
- Example: `2.5 gram`, `12.75 centimetre`

If no valid entity value is found in the image, return an empty string `""`.

## Output Format

The output file should be a CSV with the following structure:

| index | prediction |
|-------|------------|
| 1     | 2 gram     |
| 2     | 15.6 watt  |
| 3     | ""         |

- Ensure the format matches exactly with the provided sample output file (`sample_test_out.csv`).

## Evaluation Criteria

Submissions will be evaluated based on the **F1 Score**, which balances precision and recall. Predictions will be classified into one of the following categories:

- **True Positive (TP)**: OUT != "" and OUT == GT
- **False Positive (FP)**: OUT != "" and OUT != GT
- **False Positive (FP)**: OUT != "" and GT == ""
- **False Negative (FN)**: OUT == "" and GT != ""
- **True Negative (TN)**: OUT == "" and GT == ""

The **F1 score** is calculated as:

F1 score = 2 * Precision * Recall / (Precision + Recall)


Where:
- Precision = True Positives / (True Positives + False Positives)
- Recall = True Positives / (True Positives + False Negatives)

## Constraints

1. The output file **must** pass the sanity checker (`src/sanity.py`) to be evaluated.
2. Allowed units are listed in `constants.py`.
3. Ensure that there is one prediction per index in the test set.

## How to Run

1. Download the images using the `download_images` function in `src/utils.py`.
2. Build your model to predict the entity values from the images.
3. Generate a CSV output file that matches the format of `sample_test_out.csv`.
4. Run the `sanity.py` script to ensure that your output file is correctly formatted.
5. Submit your final `test_out.csv` file.

## Sample Code

A `sample_code.py` is provided to help you generate the output in the required format. Usage is optional.

## Submission

Submit the output file `test_out.csv` in the portal. The file should have the following columns:
- **index**: Unique identifier.
- **prediction**: Entity value in the format `x unit` or an empty string `""`.

Ensure that your output file passes through the sanity checker (src/sanity.py).


