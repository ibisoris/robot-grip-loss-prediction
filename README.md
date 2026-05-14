# Robot Grip Loss Prediction

This project uses machine learning to predict when a collaborative robot may lose its grip. In simple terms, the notebook looks at sensor readings from the robot, learns patterns from past examples, and tries to identify whether a future situation is likely to be a normal grip or a grip-loss event.

The main work is contained in `robot_grip_loss_prediction.ipynb`.

## Why This Matters

In collaborative robotics, a grip-loss event can interrupt production, damage an object, or create a safety concern. A prediction model can help identify risky situations earlier, giving operators or control systems more time to respond.

## Project Files

| File | Purpose |
| --- | --- |
| `robot_grip_loss_prediction.ipynb` | Main Jupyter Notebook containing the full analysis, model training, evaluation, and visualisations. |
| `dataset_02052023.xlsx` | Dataset used by the notebook. It contains robot sensor readings and the grip-loss target column. |
| `requirements.txt` | List of Python packages needed to run the notebook. |
| `.gitignore` | Tells Git which temporary or local files should not be uploaded. |

## What The Notebook Does

The notebook follows these main steps:

1. Loads the robot dataset from `dataset_02052023.xlsx`.
2. Explores the data to understand the columns, missing values, class balance, and feature distributions.
3. Converts the target column, `grip_lost`, into a machine-learning friendly format:
   - `0` means normal grip
   - `1` means grip loss
4. Removes columns that are not used as prediction features, such as identifiers and metadata.
5. Splits the data into training and testing sets.
6. Handles missing values using median imputation.
7. Scales numeric features so they are on a similar range.
8. Uses SMOTE to help with class imbalance, because grip-loss events are much less common than normal events.
9. Trains and compares machine learning models:
   - Random Forest
   - XGBoost
10. Tests both all-feature and reduced-feature versions of the dataset.
11. Tunes selected model settings using cross-validation.
12. Compares models using accuracy, precision, recall, F1-score, and AUC score.

## Results Summary

The best model selected in the notebook was:

**XGB_AllFeatures**

Its recorded test performance was:

| Metric | Score |
| --- | ---: |
| Accuracy | 0.974359 |
| Precision | 0.617021 |
| Recall | 0.591837 |
| F1-Score | 0.604167 |
| AUC Score | 0.958999 |

Accuracy is high because most examples are normal grip cases. For this project, the F1-score is especially useful because it balances how well the model finds grip-loss events with how often it raises false alarms.

## How To Run This Project

You need Python installed on your computer. Python 3.10 or newer is recommended.

### 1. Download or clone the project

If using Git:

```bash
git clone https://github.com/YOUR_USERNAME/robot-grip-loss-prediction.git
cd robot-grip-loss-prediction
```

If you downloaded the project as a ZIP file, unzip it and open the project folder.

### 2. Create a virtual environment

This keeps the project packages separate from the rest of your computer.

On Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

On macOS or Linux:

```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Install the required packages

```bash
pip install -r requirements.txt
```

### 4. Start Jupyter Notebook

```bash
jupyter notebook
```

Then open:

```text
robot_grip_loss_prediction.ipynb
```

Run the notebook cells from top to bottom.

## Dataset Note

The notebook expects the dataset file to be in the same folder as the notebook:

```text
dataset_02052023.xlsx
```

If the dataset is moved, renamed, or not included in the GitHub repository, the notebook will need to be updated with the correct file path.

Before making this repository public, make sure you are allowed to share the dataset.

## Important Terms In Plain English

**Machine learning model**: A program that learns patterns from examples and uses those patterns to make predictions.

**Feature**: A piece of information used to make a prediction, such as robot speed, current, or temperature.

**Target**: The thing the model is trying to predict. In this project, the target is whether grip was lost.

**Class imbalance**: A situation where one outcome appears much more often than another. Here, normal grip events are much more common than grip-loss events.

**SMOTE**: A method used during training to help the model learn from the smaller grip-loss class.

**Precision**: Out of the times the model predicted grip loss, how often it was correct.

**Recall**: Out of the actual grip-loss cases, how many the model found.

**F1-score**: A balanced score that combines precision and recall.

## Limitations

This project is a notebook-based machine learning analysis, not a finished production system. The model results are based on the available dataset and should be validated further before being used in a real robot environment.

Possible improvements include:

- Testing on newer or unseen robot data.
- Saving the best trained model for reuse.
- Adding a small script to run predictions outside the notebook.
- Adding more explanation of the dataset source and column meanings.
- Comparing additional models or feature engineering approaches.

## Repository Status

This project is ready to be placed on GitHub once the following are checked:

- The dataset is allowed to be shared publicly.
- Notebook outputs are either intentionally kept for readability or cleared for cleaner version control.
- The repository has been initialised with Git.
- The files have been committed and pushed to GitHub.
