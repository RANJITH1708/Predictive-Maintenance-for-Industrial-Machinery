# Predictive-Maintenance-for-Industrial-Machinery

## Overview
This project is an end-to-end machine learning solution designed to predict industrial machine failure based on real-time sensor data. The goal is to enable proactive maintenance, thereby reducing costly unplanned downtime and improving operational efficiency. The final XGBoost model successfully predicts failures with 95.6% recall and 100% precision, providing a highly reliable tool for an early-warning system.

## Problem Statement
In industrial settings, unexpected equipment failure is a primary cause of financial loss due to production halts, expensive repairs, and potential safety hazards. The traditional approach of reactive maintenance (fixing components after they break) is inefficient. This project aims to create a data-driven system that shifts the paradigm to predictive maintenance, allowing teams to address issues before a failure occurs.

## Dataset
The project utilizes the AI4I 2020 Predictive Maintenance Dataset.

### Source: [UCI Machine Learning Repository](https://www.kaggle.com/datasets/stephanmatzka/predictive-maintenance-dataset-ai4i-2020?resource=download)

Description: The dataset contains 10,000 data points with 14 features, including sensor readings like air temperature, process temperature, rotational speed, torque, and tool wear. It also includes binary flags for different failure modes.

Project Workflow
The project followed a structured, end-to-end machine learning workflow:

Environment Setup: A virtual environment was created to manage project dependencies, which are listed in the requirements.txt file.

Exploratory Data Analysis (EDA): An initial analysis was performed to understand the data's structure. Key findings included a significant class imbalance (only 3.4% of instances were failures) and strong correlations between certain features. A pairplot visually confirmed that failures tend to occur in a "danger zone" of high torque and low rotational speed.

<img width="865" height="741" alt="image" src="https://github.com/user-attachments/assets/b9da33e6-f509-4168-afb4-77226357e866" />


## Feature Engineering:

The categorical Type feature was one-hot encoded.

Two new, physically meaningful features were created: Power [W] (product of torque and speed) and Temp_Diff [K] (difference between process and air temperature).

## Model Development:

Data Splitting: The data was split into training (80%) and testing (20%) sets, using stratification to maintain the class imbalance in both sets.

Scaling: Features were scaled using StandardScaler to ensure model performance was not skewed by features with different ranges.

Model Selection: An XGBoost Classifier was chosen for its high performance on tabular data. The scale_pos_weight parameter was used to compel the model to pay extra attention to the rare failure class.

Model Evaluation & Interpretation: The trained model was evaluated on the unseen test set. A confusion matrix was used to analyze its predictive accuracy, and the SHAP (SHapley Additive exPlanations) library was used to interpret the model's decisions and identify key feature importances.

Productionizing: The final trained model and the data scaler were saved as .pkl files using joblib, making them ready for deployment in a real-world application.

## Key Findings & Results
Model Performance: The final model demonstrated exceptional performance on the test data.

Recall: 95.6% (Of 68 actual failures, 65 were correctly identified).

Precision: 100% (There were zero false alarms).

Missed Failures (False Negatives): Only 3.

<img width="576" height="432" alt="image" src="https://github.com/user-attachments/assets/11ef4721-eb38-4b6e-90ef-3f0acff7b130" />


## Feature Importance: SHAP analysis confirmed the findings from EDA. The most influential features in predicting failure were Torque, Rotational Speed, our engineered Power feature, and specific failure type flags.
<img width="778" height="700" alt="image" src="https://github.com/user-attachments/assets/3f1ee635-d978-4501-bf84-aec266f5da37" />


## Tools & Technologies
Language: Python 3.12

## Libraries:

Pandas & NumPy (Data Manipulation)

Matplotlib & Seaborn (Data Visualization)

Scikit-learn (Data Preprocessing & Evaluation)

XGBoost (Modeling)

SHAP (Model Interpretation)

Joblib (Model Saving)

## Environment: VS Code with Jupyter Notebooks

## How to Run This Project
### Clone the repository:

Bash

git clone <your-repository-url>
Create and activate a virtual environment:

Bash

python -m venv .venv
.\.venv\Scripts\Activate
Install the required dependencies:

Bash

pip install -r requirements.txt
Run the Jupyter Notebook:
Open the failure_analysis.ipynb file in VS Code or Jupyter and execute the cells.

## Conclusion
This project successfully demonstrates the development of a highly effective predictive maintenance model. The final artifact is a reliable tool that can be integrated into an industrial monitoring system to provide early warnings of equipment failure, enabling proactive maintenance and delivering significant business value.