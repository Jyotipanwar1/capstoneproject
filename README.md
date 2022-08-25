# Salary prediction for engineering graduates

# PROBLEM SATATEMENT
Given a new student profile, can we predict the salary of the engineer based on the historic and AMCAT data.
AMEO 2015 has gained traction since its public release. Aspiring Minds annually publishes the National Employability Report, a data-driven commentary on graduates and their employability. A recent NER was based on an extension of this dataset. It was also analyzed as part of two data challenges - at ASSESS 2015, a workshop on data-driven assessments held at ICDM 2015 and at IKDD CODS 2016. As part of the challenge, researchers from industry and academia predicted annual salaries of engineering graduates. The challenge also had them interpret the factors determining salaries and had them visualize the dataset to infer insights. The dataset has a variety of input formats, including semi-structured text in the form of job titles, making it a rich instructional tool which students and professionals can readily relate to and learn from. It can also be used to teach quantitative social science methods.

# DATA DESCRIPTION
 
The dataset consists of 27 numerical , 10 categorical and 2 datetime attributes . The ‘Salary’ attribute is used as the target variable.
For every engineer, AMEO dataset provides anonymized bio data information along with their respective skill scores and employment outcome information. Specifically, the following information is available for every engineer: 
Personal information like gender and date of birth.  Pre-university information like 10th and 12th grade marks, board of education and 12th grade graduation year. 
 University information like GPA, college major, college reputation proxy, graduation year and college location. 
The dataset consists of shape belonging to 3998 rows and 39 columns.
 
# Data preprocessing steps and EDA :
There are null values present in the dataset which are present in columns ‘Job City’, ‘10board’, ‘12board’ that are hidden either in form of  0 or -1.
The  categorical columns includes ‘Designation’, ‘Job City’, ‘10board’, ‘12board’  consist of lot of sub-categories that were rendered with specific categories. 
With the columns ‘DOJ’ and ‘DOL’ we have evaluated the new column as ‘Experience’.
-1 present in the dataset (excluding ‘Job City’ ) represents student haven’t appeared for the examination.
After the pre-processing steps we done some observations on numerical and categorical columns like 
*Designation :There were 160 different designations ,Approx. 53% of them belongs to engineering field,17% developers, 10% Analyst.
 For 10th and 12th percentage We classified the percentage under the universal divisions:
4- denotes percentage less than 50 i.e. Fourth Division,3- denotes percentage >50 and <=65 i.e. Third Division ,2- denotes percentage >65 and <=80 i.e. second Division
1- denotes percentage >80 i.e. First Division.
for Age column ,We have converted the date of birth into age by using 31 dec 2015 as present date and for College State ,There were 26 states that has been bifurcated to Zones. Majority of employees have done there Grads from North-Indian states.

# Feature Engineering
Creating YOE (years of experience feature using DOJ & DOL adn Creating AGE feature using DOB feature anddate at which the data was collected i.e. 31-12-2015 .
Creating “Subject Total” feature using the sum of subject marks of the candidate and then scaled it.

# Feature Extraction and Feature Selection
We created a function for feature extraction and feature selection which gave us best selected features in output.
The function returns list of redundant features on the basis of five different techniques these are:
P value-  Sequential Feature Selector-.  Recursive Feature Elimination-Random Forest Feature Importance
The feature selection was done by dropping  redundant features that come out be redundant in most of these techniques and if the adjusted R2 score raises  we end up dropping a feature in that iteration
College City Tier , 10Board,12Board, Domain, Openness to Experience, most of these features had high P value.
In Anova test in one of iteration College State and Gender were coming out to be redundant but we didn’t drop the Gender because it led to decrease in Adjusted R2 score and had low P value in OLS.
Some features we dropped on the basis of multicollinearity and these features were also had high pvalue. These were Age and Years since graduated these features were correlated to Experience column and Experience contributed more to modelling and made high business sense.
We also tried to restructure categorical variables which were redundant, and were insignificant in anova test like we tried to combine the columns of College state to make North South East and West in subsequent Iterations and it didn’t help so we dropped them.There was imbalance in categorization of degree where B.Tech folks were very high in number . So, we segregated them into Undergraduate(UG) and combining all the Master’s stream into  Post graduate(PG) and  it came out to be significant. 

# Model Building
We performed transformation on our Data and after that we scaled our data using Standard Scalar on our numerical data and encoded our data using One hot encoding.
We also did capping on our data with lower limit 0.05 and Upper limit as 0.095.
We chose OLS model as our base model and we fitted our model and  did cross-validation and found out that our Mean Test R2 came out to be 0.46 and our Mean Test Adjusted R2 was 0.436.
Mean Train R2 was 0.472.

# Model selection
In our analysis, we found out that average test score after hyper parameter tuning and cross-validation for Linear Regression and Gradient Boosting are similar.
Because Linear Regression analysis gives better understanding of statistical inference overall and it has very good interpretability in terms of the contribution of each predictor w.r.t target variable.
While gradient boosting which is considered more of a black box where there is less interpretability and reliability
All the tree based models did not do any good in predictive modelling for our dataset.
Hence, we decide Linear Regression as our final model.

