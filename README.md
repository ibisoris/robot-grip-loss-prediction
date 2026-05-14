# Robot Grip Loss Prediction

This project uses machine learning to predict when a collaborative robot may lose its grip. In simple terms, the notebook looks at sensor readings from the robot, learns patterns from past examples, and tries to identify whether a future situation is likely to be a normal grip or a grip-loss event.

The main work is contained in `robot_grip_loss_prediction.ipynb`.

## Project Highlights

- Uses real robot sensor data to study grip-loss behaviour.
- Includes exploratory data analysis with charts and summary statistics.
- Handles an imbalanced target, where grip-loss cases are much less common than normal grip cases.
- Builds a complete machine learning workflow using preprocessing, SMOTE, model training, tuning, and evaluation.
- Compares Random Forest and XGBoost models.
- Presents results in a notebook format so the analysis can be followed step by step.

## Why This Matters

In collaborative robotics, a grip-loss event can interrupt production, damage an object, or create a safety concern. A prediction model can help identify risky situations earlier, giving operators or control systems more time to respond.

## Problem Statement

The goal of this project is to answer the question:

> Can robot sensor readings be used to predict whether a grip-loss event is likely to occur?

This is treated as a binary classification problem. The model predicts one of two possible outcomes:

- `0`: normal grip
- `1`: grip loss

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

## Methodology

The project uses a standard supervised machine learning approach:

| Stage | What Happens |
| --- | --- |
| Data loading | The Excel dataset is loaded into a pandas DataFrame. |
| Data exploration | The notebook checks the dataset shape, column names, missing values, distributions, and class balance. |
| Preprocessing | Missing values are filled using the median, and numeric features are scaled. |
| Class imbalance handling | SMOTE is used on the training data to help the model learn from the less common grip-loss cases. |
| Model training | Random Forest and XGBoost classifiers are trained and compared. |
| Feature reduction | Highly correlated features are removed in one experiment to reduce redundancy. |
| Hyperparameter tuning | Grid search with stratified cross-validation is used to test selected model settings. |
| Evaluation | Models are compared using accuracy, precision, recall, F1-score, and AUC score. |

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

## How To Interpret The Results

The model performs very well at identifying normal grip cases. Grip-loss cases are harder to predict because they appear much less often in the dataset.

The best model found a useful balance between:

- detecting actual grip-loss events
- avoiding too many false grip-loss alarms

In a real robotics setting, this balance would need to be chosen carefully. Missing a true grip-loss event may be more serious than raising a false warning, depending on the safety and production requirements.

## How To Run This Project

You need Python installed on your computer. Python 3.10 or newer is recommended.

### 1. Download or clone the project

If using Git:

```bash
git clone https://github.com/ibisoris/robot-grip-loss-prediction.git
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

This project uses a public robot sensor dataset. The dataset remains subject to the terms of its original source. It is included here for educational and reproducibility purposes.

If the dataset is moved, renamed, or not included in the GitHub repository, the notebook will need to be updated with the correct file path.

## Technologies Used

- Python
- Jupyter Notebook
- pandas
- NumPy
- Matplotlib
- Seaborn
- scikit-learn
- imbalanced-learn
- XGBoost
- openpyxl

## Important Terms In Plain English

**Machine learning model**: A program that learns patterns from examples and uses those patterns to make predictions.

**Feature**: A piece of information used to make a prediction, such as robot speed, current, or temperature.

**Target**: The thing the model is trying to predict. In this project, the target is whether grip was lost.

**Class imbalance**: A situation where one outcome appears much more often than another. Here, normal grip events are much more common than grip-loss events.

**SMOTE**: A method used during training to help the model learn from the smaller grip-loss class.

**Precision**: Out of the times the model predicted grip loss, how often it was correct.

**Recall**: Out of the actual grip-loss cases, how many the model found.

**F1-score**: A balanced score that combines precision and recall.

**AUC score**: A score that shows how well the model separates the two classes overall.

## Limitations

This project is a notebook-based machine learning analysis, not a finished production system. The model results are based on the available dataset and should be validated further before being used in a real robot environment.

Possible improvements include:

- Testing on newer or unseen robot data.
- Saving the best trained model for reuse.
- Adding a small script to run predictions outside the notebook.
- Adding more explanation of the dataset source and column meanings.
- Comparing additional models or feature engineering approaches.
- Adding model explainability, such as feature importance or SHAP analysis.
- Packaging the best model so it can be loaded and reused without rerunning the full notebook.

## Future Work

Useful next improvements would be:

- Add the exact dataset source link.
- Add a license file if the project is intended for reuse.
- Save the best-performing trained model.
- Create a simple prediction script for new robot sensor readings.
- Add more discussion of which sensor features are most important.
- Test the model on new data collected at a different time.
