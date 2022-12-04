# Business_Analytics
It is a team project for the year 3 module, Business Analytics from Seoul Tech.

Goal : To define a problem and use data analysis to solve it.

Topic : Prediction of Integration And Abolition for University

### 1. [Dataset][link]
[link]: https://github.com/jeewonkimm2/Business_Analytics/tree/main/Data


1. [Filtered government sponsorship university list][link2]

[link2]: https://github.com/jeewonkimm2/Business_Analytics/tree/main/Data/Filtered_University
- This dataset has 3 columns, Year, University, and Gov_Sponsorship.
- Our team manually collected separate dataset from Korea Development Institute and editted into one file.
  - Year : The year of evaluation
  - University : The name of university
  - Gov_Sponsorship
    - 1 : Government sponsorship
    - 0 : No government sponsorship

2. [Progress dataset][link3]

[link3]: https://github.com/jeewonkimm2/Business_Analytics/tree/main/Data/Progress_Merged_data

+ Year : Year information for each admission
+ Region : Region information for each school
+ Departmental Affiliation : A major classification of departmental affiliations
+ The number to be admitted : Information on students admitted by departments
+ Candidate : The number of candidates
+ The number of admissions : Information on students who admitted
+ Government financial support
    - 1 : Existence of government financial support
    - 0 : No existence of government financial support
+ School & Department : Information merged on school and each department
+ Competition rate : Information derived from dividing the number of applicants by the number to be admitted
+ Total fertility rate : Information on fertility rate by each region
+ Net mover : Information on net mover by each region
+ Immigration : Information on the number of immigration



3. [Final dataset][link4]

[link4]: https://github.com/jeewonkimm2/Business_Analytics/tree/main/Data/Final_dataset


  + Year : Year information for each admission
  + Region : Region information for each school
  + Departmental Affiliation (major series) : A major classification of departmental affiliations 
  + Departmental Affiliation (middle series) : A middle classification of departmental affiliations 
  + The number to be admitted : Information on students admitted by departments
  + Candidate : The number of candidates
  + The number of admissions : Information on students who admitted
  + Government financial support
      - 1 : Existence of government financial support
      - 0 : No existence of government financial support
  + Awareness : Information on awareness of departmental affiliations to students by each year
  + School & Department : Information merged on school and each department
  + Competition rate : Information derived from dividing the number of applicants by the number to be admitted
  + Total fertility rate : Information on fertility rate by each region
  + Net mover : Information on net mover by each region
  + Immigration : Information on the number of immigration
  + Schoolage : Information on schoolage population by each year





### 2. [Progress Phase][link5]
[link5]: https://github.com/jeewonkimm2/Business_Analytics/tree/main/Progress

설명필



### 3. [Final Phase][link6]
[link6]: https://github.com/jeewonkimm2/Business_Analytics/tree/main/Final

1. 
추가




2. Model training and predicting result

- File Name : main_training.ipynb
- Independent variables(X) : '연도','시도','대계열','중계열','모집인원_학부계','Gov_Spnsorship','awareness','Total_fertility_rate','Net_Mover','immigration','schoolage'
- Target variable(y) : '지원자_전체_계'
- Model Selection : GridSearchCV(KFold when n_splits is 5) and train_test_split(Train, Test, and Validation)
- Preprocessing with ColumnTransformer
  - Numeric features : '모집인원_학부_계','Total_fertility_rate','Net_Mover','immigration','schoolage'
    - We used polynomialfeatures with degree 2 and standardscaler.
  - Categorical features : '연도','시도','대계열','중계열','Gov_Spnsorship','awareness'
    - We used onehotencoder.
- Pipeline combining preprocessor
  1. When fit is **LinearRegression**
      - r2 score : 0.622863334546101
  2. When fit is **LassoRegression**
      - r2 score : 0.6232647986187436
  3. When fit is **RidgeRegression**
      - r2 score : 0.6228460532502517
  4. When fit is **GradientBoostingRegressor**
      - r2 score : 0.6961511258186199
  5. When fit is **RandomForestRegressor**
      - r2 score : 0.6447984110664
  6. When fit is **SupportVectorRegression**
      - r2 score : 0.6116517939646415
  7. When fit is **KernelRidgeRegression**
      - r2 score : 0.6363528761071908
- <U> Conclusion from model training </U>
  - **GradientBoostingRegressor** performed the best on our dataset with parameters {'fit__loss': 'ls', 'fit__max_depth': 7, 'fit__max_features': 'sqrt', 'fit__min_samples_split': 6}
- Applying on test dataset
  - r2 score : 0.9192784570251001
  
  
2. Predicting future admission
- File Name : main_training.ipynb
- Phase
  - Importing future dataset for future independent variables.
  - Applying the best model and hyperparameters we obtained from previous step.
  - A type of target variable['지원자_전체_계'] was changed into integer because it is counting the number of human.
  - We could obtain 'competition_rate' rate, which is our final goal, dividing '지원자_전체_계' into '모집인원_학부_계'
  - Extracted the data into excel for visualization.

### 5. [Visualization][link]
[link4]: https://github.com/jeewonkimm2/Business_Analytics/tree/main/Visualization  

![conclusion_image](https://github.com/jeewonkimm2/Business_Analytics/blob/main/Visualization/map_image.png)  
#### Average university competitiveness by region in 2026  

![conclusion_image](https://github.com/jeewonkimm2/Business_Analytics/blob/main/Visualization/pie_chart.png)  
#### Additional analysis of Jeju with the lowest average competitiveness and Incheon with the highest average competitiveness  

![conclusion_image](https://github.com/jeewonkimm2/Business_Analytics/blob/main/Visualization/image.png)  
#### The list of universities with poor competency and the number of times selected for each year  
