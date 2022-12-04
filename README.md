# [Business Analytics Term Project]

## Overview
- It is a term project for the year 3 module, Business Analytics. We needed to find any problem that can be solved by data mining techniques in one of business domains.

- Topic : Prediction of integration and abolition for university.

- Goal : To predict departments that might be integrated or abolished using competition rate for each department of schools.

### 1. Background
- A trend of decreasing the school-age population and the number of students eligible for admission.
<img width="423" alt="image" src="https://user-images.githubusercontent.com/108987773/205484547-e6a3a80a-b0bf-4f08-83d3-3842f91fd397.png">
  
- Trends in integration and abolition of university departments is increasing in South Korea.
<img width="407" alt="image" src="https://user-images.githubusercontent.com/108987773/205484592-5adcd29a-8e45-4a8f-997d-d1fec2b04557.png">
  
**<U>As the number of students decreased, the restructuring of universities was also being carried out intensively.</U>**

- Expected Effect
  - For Student : The predictions can be considered when selecting a university to go.
  - For University : With the predictions, universities can know the position of themselves and prepare for changing phenomenons.


### 2. [Dataset][link]
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



3. [Future dataset][link8]

[link8]: https://github.com/jeewonkimm2/Business_Analytics/tree/main/Data/Final_dataset

- File Name : future.csv



4. [Final dataset][link4]

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







### 3. [Obtaining best model and hyperparameters][link6]
[link6]: https://github.com/jeewonkimm2/Business_Analytics/tree/main/Final

1. Model training and predicting result

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
  - **GradientBoostingRegressor** performed the best on our dataset with **hyperparameters {'fit__loss': 'ls', 'fit__max_depth': 7, 'fit__max_features': 'sqrt', 'fit__min_samples_split': 6}**
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

### 4. [Visualization and Conclusion][link7]
[link7]: https://github.com/jeewonkimm2/Business_Analytics/tree/main/Visualization

![conclusion_image](https://github.com/jeewonkimm2/Business_Analytics/blob/main/Visualization/map_image.png)
#### Average competitiveness by region in 2026  
The larger the size of the circle on the map, the higher the mean. You can check the area and figures according to the color on the right side of the map.  

![conclusion_image](https://github.com/jeewonkimm2/Business_Analytics/blob/main/Visualization/pie_chart.png)
#### Additional analysis of Jeju with the lowest average competitiveness and Incheon with the highest average competitiveness  
We analyzed Incheon with the highest average and Incheon with the lowest average in detail. While 65% of all universities in Jeju Island belong to the bottom 20% group, there were no universities belonging to the group in Incheon. Also, 74.2% of universities in Incheon are in the top 40% group.  We think that the geographical disadvantage of Jeju has resulted in this.  

![conclusion_image](https://github.com/jeewonkimm2/Business_Analytics/blob/main/Visualization/image.png)
#### The list of departments with poor competency and the number of times selected for each year  
The departments on this list are in danger of being eliminated due to lack of competitiveness. In particular, in the case of Gyeongju University's_special physical education department, the risk of disappearing is very high, so it is recommended not to enter.  
