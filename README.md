![](UTA-DataScience-Logo.png)

# Springleaf Marketing Response

* This repository houses an attempt to predict which customers will respond to a direct mail offer provided by Springleaf. 

## Overview

* Objective: The goal of this project is to predict whether a potential customer will respond to a direct mail offer. Springleaf aims to support individuals by offering accessible personal and auto loans designed to help them take control of their financial lives. By analyzing anonymized customer data, the objective is to develop a machine learning model capable of identifying likely responders to such offers.
* Dataset Sampling and Preprocessing: Due to the large size of the original dataset, a random sample of 1,000 records was selected for analysis. To minimize class imbalance, the sample was stratified by selecting 500 instances with a target value of 1 (responders) and 500 with a target value of 0 (non-responders). While this method may not be the most sophisticated approach to class balancing, it provided improved results compared to purely random sampling. After sampling, extensive data cleaning was conducted to remove irrelevant or low-variance features and prepare the data for training.
* Model Training and Evaluation: A Random Forest Classifier was used for model training. Model performance was evaluated using accuracy, ROC-AUC score, and corresponding classification metrics. The best model achieved an accuracy of 71% and a ROC-AUC score of 0.76. While these results are promising, there is still room for further optimization and improvement.

## Summary of Workdone


### Data

* Data:
  * Type: CSV file that has been anonymized to protect customer info.
    * Input: Tons of data including state, zipcode, timestamps, etc. The columns are all named VAR_0001, VAR_0002, etc. making it really hard to know what type of data it is.
  * Size: The total size is (145231, 1934) what my computer could handle was (1000, 1934) which is still a bit large.
  * split: The full data set is unbalanced where no is the majority and yes is minority. I used an 80/20 split when training

#### Preprocessing / Clean up

* This data was very "messy", for the sample I took there were a total of 17954 total 'NaN' not count '-1','','-999999'. Another issue with replacing the alternative versions for null is some variables had -1 as a item meant to be in the data set as something other than 'NaN'. Removing duplicates was the first step, second, split the data into x (numerical and categorical) and y (target) while dropping 'ID' variable along the way. Next I changed all numeric value to float, then split categorical and numerical data into different data frames. Now that the data types are split I clip the upper and lower bound of the numeric columns to rid the data of outliers. There were columns that only contain 'NaN' those need to be dropped in order to avoid issues. Now that this is done impute, scaler, and one hot enconde all data and concatenate the results into a new data frame ready for training. 

#### Data Visualization
There are lots of numerical values that are highly correlated. This data was so large and hard to interpret due to the columns being named VAR_0001, etc.
![](correlation-heat-map-of-numericals.png)

### Problem Formulation

* Define:
  * Input: The data that was intputed was everything remaining after the cleaning. Without references are for the columns it was difficult picking specific inputs
    Output: Binary Classification (1 yes & 0 no)
  * Models: Models used are decision tree, random forest classifier, and Linear discriminant analysis.
  * Loss, Optimizer, other Hyperparameters:
    The models use accuracy as the evaluation metric as well as confusion matrix.

### Training

* Describe the training:
Training
  * Approach: The model was trained using a Random Forest Classifier consisting of 100 decision trees.
  *	Training Time: Training was efficient and completed within a few minutes.
  * Stopping Criteria: The model was trained until convergence, using the default fitting process provided by the algorithm.
  * Challenges: The primary challenge was ensuring proper data cleaning and preprocessing, which was essential for improving model performance and achieving reliable results.

### Performance Comparison
Random Forest
![](Random-forest.png)

Decision Tree
![](Decision-tree.png)

LDA
![](LDA.png)


### Conclusions

Decision tree worked the best compared to the others I used.

### Future Work

In future projects, I would prefer to begin with a smaller dataset to focus more effectively on analysis and modeling. I underestimated the time and effort required for data cleaning, which took up the majority of this project. Despite the challenges, working with this dataset was a valuable learning experience that taught me a great deal about data preparation and analysis. As I progress in my data science education, I intend to revisit this dataset to apply new skills and make further improvements to achieve more accurate and insightful results.
## How to reproduce results

* In order to obtain this data you have join the competition. Link: https://www.kaggle.com/competitions/springleaf-marketing-response
   * To reproduce my results simply download spring leaf data cleaning file, and down load the data set. Once you have the data set, if your computer can not handle it you will have to sample it out using google colab or your desired choice. 
   * This data code can also be used for other set as well, there may be some tweaks that need to be made but nothing major.
* I would suggest using Jupyter only because colab will delete your files when you leave. If you have a very weak computer or no memory I would suggest using colab.

### Overview of files in repository

* Describe the directory structure, if any.
* List all relavent files and describe their role in the package.
* An example:
  * utils.py: various functions that are used in cleaning and visualizing data.
  * preprocess.ipynb: Takes input data in CSV and writes out data frame after cleanup.
  * visualization.ipynb: Creates various visualizations of the data.
  * models.py: Contains functions that build the various models.
  * training-model-1.ipynb: Trains the first model and saves model during training.
  * training-model-2.ipynb: Trains the second model and saves model during training.
  * training-model-3.ipynb: Trains the third model and saves model during training.
  * performance.ipynb: loads multiple trained models and compares results.
  * inference.ipynb: loads a trained model and applies it to test data to create kaggle submission.

* Note that all of these notebooks should contain enough text for someone to understand what is happening.

### Software Setup
* I accessed all software through libraries.
* For data understanding/processing use numpy, pandas and matplotlib.
* For training Use sklearn list of packages:
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import OneHotEncoder, StandardScaler, FunctionTransformer
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, classification_report, roc_auc_score, confusion_matrix
from sklearn.linear_model import LogisticRegression
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier
from sklearn.discriminant_analysis import LinearDiscriminantAnalysis
from sklearn.feature_selection import mutual_info_classif, VarianceThreshold
from sklearn.compose import ColumnTransformer
from sklearn.metrics import roc_curve, auc

If you have any feed back or suggestions for improvement contact me at:
pms6896@mavs.uta.edu







