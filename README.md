# DASHBOARD-DEVELOPMENT

COMPANY: CODTECH IT SOLUTIONS

NAME:KHUSHI SHAH

INTERN ID:CT04DL131

DOMAIN:DATA ANALYTICS

DURATION:4 WEEKS

MENTOR:NEELA SANTHOSH

## DESCRIPTION

This Python script presents a complete machine learning pipeline for predicting the likelihood of diabetes using the Pima Indians Diabetes dataset. The workflow follows a structured approach encompassing data loading, exploratory data analysis (EDA), preprocessing, feature selection, model training, and evaluation.

#### 1. **Importing Libraries**

The script begins by importing essential Python libraries:

* `pandas` and `numpy` for data manipulation.
* `seaborn` and `matplotlib.pyplot` for data visualization.
* Scikit-learn modules for preprocessing, feature selection, model training, and evaluation.

#### 2. **Loading the Dataset**

The dataset is read using `pandas.read_csv()`, and column names are explicitly defined for clarity. The dataset contains several health-related measurements for female patients, including `Pregnancies`, `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, `BMI`, `DiabetesPedigreeFunction`, `Age`, and the target variable `Outcome`, which indicates the presence (1) or absence (0) of diabetes.

#### 3. **Exploratory Data Analysis (EDA)**

Basic EDA is conducted using `head()` to inspect the top records and `describe()` to get statistical summaries. Additionally, a count plot using `seaborn` visualizes the distribution of the target classes (`Outcome`). This helps to understand class imbalance and overall data characteristics.

#### 4. **Feature Selection and Preprocessing**

The dataset is split into features (`X`) and target (`y`). Feature normalization is performed using `StandardScaler` to standardize the values, ensuring that all features contribute equally to the learning algorithm. Next, `SelectKBest` with the `f_classif` scoring function is applied to select the top 5 most relevant features based on statistical significance. This step reduces dimensionality, potentially improving model performance and interpretability. The selected feature names are printed for reference.

#### 5. **Train/Test Split**

The dataset is split into training and testing sets using `train_test_split` with an 80-20 split. This separation ensures that the model can be evaluated on unseen data, providing an unbiased assessment of its performance.

#### 6. **Model Training**

A `RandomForestClassifier`, a robust ensemble learning algorithm, is trained on the selected and scaled features. Random forests operate by constructing multiple decision trees and averaging their predictions, offering strong performance and resilience to overfitting.

#### 7. **Model Evaluation**

The model's predictions on the test data are evaluated using several metrics:

* **Confusion Matrix**: Provides the count of true positives, true negatives, false positives, and false negatives.
* **Classification Report**: Displays precision, recall, F1-score, and support for each class.
* **Accuracy Score**: Shows the overall accuracy of the model.

This evaluation helps in understanding how well the model is distinguishing between diabetic and non-diabetic individuals.



 Pregnancies  Glucose  BloodPressure  SkinThickness  Insulin   BMI  \
0            6      148             72             35        0  33.6   
1            1       85             66             29        0  26.6   
2            8      183             64              0        0  23.3   
3            1       89             66             23       94  28.1   
4            0      137             40             35      168  43.1   

   DiabetesPedigreeFunction  Age  Outcome  
0                     0.627   50        1  
1                     0.351   31        0  
2                     0.672   32        1  
3                     0.167   21        0  
4                     2.288   33        1  
       Pregnancies     Glucose  BloodPressure  SkinThickness     Insulin  \
count   768.000000  768.000000     768.000000     768.000000  768.000000   
mean      3.845052  120.894531      69.105469      20.536458   79.799479   
std       3.369578   31.972618      19.355807      15.952218  115.244002   
min       0.000000    0.000000       0.000000       0.000000    0.000000   
25%       1.000000   99.000000      62.000000       0.000000    0.000000   
50%       3.000000  117.000000      72.000000      23.000000   30.500000   
75%       6.000000  140.250000      80.000000      32.000000  127.250000   
max      17.000000  199.000000     122.000000      99.000000  846.000000   

              BMI  DiabetesPedigreeFunction         Age     Outcome  
count  768.000000                768.000000  768.000000  768.000000  
...
25%     27.300000                  0.243750   24.000000    0.000000  
50%     32.000000                  0.372500   29.000000    0.000000  
75%     36.600000                  0.626250   41.000000    1.000000  
max     67.100000                  2.420000   81.000000    1.000000  


![image](https://github.com/user-attachments/assets/3633076a-ea01-44f9-9c31-7b2390b4694a)

Selected features: ['Pregnancies', 'Glucose', 'BMI', 'DiabetesPedigreeFunction', 'Age']

Confusion Matrix:

 [[81 18]
 [17 38]]
 
Classification Report:

               precision    recall  f1-score   support

           0       0.83      0.82      0.82        99
           1       0.68      0.69      0.68        55

    accuracy                           0.77       154
    
   macro avg       0.75      0.75      0.75       154
weighted avg       0.77      0.77      0.77       154

Accuracy Score: 0.7727272727272727

