# cementStrengthPrediction
we have to identify the how much pressure can handle one meter cube of that concrete block
<br><br>
# [DEMO](#demo)
# Index

* [Problem statement](#problem-statement)
* [Goal of this Project](#goal-of-this-Project)
* [Glimpse of Dataset](#glimpse-of-Dataset)

### EDA
* [Check the missing values](#Check-the-missing-values)
* [Data Distribution](#data-distribution)
* [Data Transformation](#data-transformation)
* [check for outliers](#check-for-outliers) 
* [Features related with Target column](#features-related-with-target-column)
* [Correaltion using Heatmap](#correaltion-using-heatmap)



### Training Data Description
* [Architecture](#architecture)
* [Data Description](#data-description)
* [Data Validation](#data-validation) 
* [Data Insertion in Database](#data-insertion-in-database)
* [Model Training](#model-training) 

### Prediction Data Description
* [Data Validation](#data-validation1)  
* [Data Insertion in Database](#data-insertion-in-database1) 
* [Prediction](#prediction)

### Logging
- ### Each and every step it will log in Mongo Db
* [Training Logs](#training-logs)
* [Prediction Logs](#prediction-logs)

## Demo
- Check Here Live Demo: (https://rocky-peak-81548.herokuapp.com/)

## Problem Statement
### our problem statement is to predict the compressive strength of a cement block

### compressive strength: **how much pressure that one meter cube of that concrete block can handle**
<br>
<br>


## Goal of this Project
### Why we need this?
**Suppose you are building something very tall building, bridges. They need to handle a lot of pressure if the block is not going to good. Then your structure won't be durable.
They won't be able to bear the road that they are designed to hold. That's the reason we need the compressive strength of cement. the problem statement is based on the quantity of different materials**
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

# Exploratory Data Analysis (EDA)  
<br>
<br>
  
  
  



## Check the missing values

* There is no missing value
  <p align="center">
<img src="https://github.com/rahulk15/images/blob/main/cement%20missing%20values.png" alt="command">
</p>
<br>
<br>
<br>
<br>

## Data Distribution

### For Some column, there is some skewness present in the data.
  <p align="center">
<img src="https://github.com/rahulk15/images/blob/main/cement%20Data%20Dirsibution.png" alt="command">
</p>
<br>
<br>
<br>
<br>

## Data Transformation
#### To remove this Skewness, we are doing log transformation.
#### Before doing log transformation, let's add 1 to each value in every column. because some of the columns of values are Zero so that we don't get an exception while calculating the log for value 0
* Here is the code :
<p align="center">
<img src="https://github.com/rahulk15/images/blob/main/code%20of%20log%20transformation.png" alt="command">
</p>

#### After Data transformation. a Data is in lot better shape than the previous
<p align="center">
<img src="https://github.com/rahulk15/images/blob/main/log%20transfromation.png" alt="command">
</p>
<br>
<br>
<br>
<br>

## check for outliers
#### Mostly our data is good. very less outliers are there. so don't need to remove
<p align="center">
<img src="https://github.com/rahulk15/images/blob/main/outliers.png" alt="command">
</p>
<br>
<br>
<br>
<br>


## Features related with Target column
#### The relationship doesn't look particularly linear, but we will try using Linear Regression and see how it works on our data. We will also use a Random forest regressor and compare our results from both models.
<p align="center">
<img src="https://github.com/rahulk15/images/blob/main/cement%20correltion.png" alt="command">
</p>
<br>
<br>
<br>
<br>

## Correaltion using Heatmap
Highest correltion betwen features is 0.62
#### None of our columns seems to be correlated.
<p align="center">
<img src="https://github.com/rahulk15/images/blob/main/cement%20coreation%20with%20headmap.png" alt="command">
</p>
<br>
<br>
<br>
<br>


## Architecture
<p align="center">
<img src="https://github.com/rahulk15/images/blob/main/cement%20architecture.png" alt="command">
</p>
<br>
<br>
<br>
<br>



## Data Description
#### Given is the variable name, variable type, the measurement unit and a brief description. 
#### The concrete compressive strength is the regression problem. The order of this listing 
#### corresponds to the order of numerals along the rows of the database. 


 |Name  	| Data Type   |	 Measurement 	| Description|
| -------------------| ------------- | ------------- |-----------|
|Cement (component 1)|quantitative|kg in a m3 mixture|Input Variable|
| Blast Furnace Slag (component 2)  | quantitative  |kg in a m3 mixture|Input Variable-- Blast furnace slag is a nonmetallic coproduct produced in the process. It consists 								primarily of silicates, aluminosilicates, and calcium-alumina-silicates|
| Blast Furnace Slag (component 2)  |quantitative|kg in a m3 mixture|Input Variable- it is a coal combustion product that is composed of the particulates (fine particles of 											burned fuel) that are driven out of coal-fired boilers together with the flue gases. |
|Water (component 4)| quantitative  |kg in a m3 mixture|Input Variable|
| Superplasticizer (component 5)  | quantitative|kg in a m3 mixture|Input Variable--Superplasticizers (SP's), also known as high range water reducers, are additives used in 								making high strength concrete. Their addition to concrete or mortar allows the reduction of the water to cement ratio 								without negatively affecting the workability of the mixture, and enables the production of self-consolidating concrete 									and high performance concrete|
|Coarse Aggregate (component 6)|quantitative	|kg in a m3 mixture|Input Variable-- construction aggregate, or simply "aggregate", is a broad category of coarse to medium 					grained particulate material used in construction, including sand, gravel, crushed stone, slag, recycled concrete and geosynthetic aggregates|
|Fine Aggregate (component 7)|quantitative|kg in a m3 mixture|Input Variable—Similar to coarse aggregate, the constitution is much finer.|
|Age|quantitative|Day (1~365)|Input Variable|
|Concrete compressive strength|	quantitative|MPa|Output Variable|
<br>
<br>
<br>
<br>


## Data Validation 
#### Apart from training files, we also require a "schema" file from the client, which contains all the relevant information about the training files such as: Name of the files, Length of Date value in FileName, Length of Time value in FileName, Number of Columns, Name of the Columns, and their datatype.
### In this step, we perform different sets of validation on the given set of training files.  
#### 1. Name Validation- We validate the name of the files based on the given name in the schema file. We have created a regex pattern as per the name given in the schema file to use for validation. After validating the pattern in the name, we check for the length of date in the file name as well as the length of time in the file name. If all the values are as per requirement, we move such files to ["Good_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Good_Raw) else we move such files to ["Bad_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Bad_Raw).
#### 2. Number of Columns - We validate the number of columns present in the files, and if it doesn't match with the value given in the schema file, then the file is moved to ["Bad_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Bad_Raw).
#### 3. Name of Columns - The name of the columns is validated and should be the same as given in the schema file. If not, then the file is moved to ["Bad_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Bad_Raw).
#### 4. The datatype of columns - The datatype of columns is given in the schema file. This is validated when we insert the files into Database. If the datatype is wrong, then the file is moved to ["Bad_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Bad_Raw).
#### 5. Null values in columns - If any of the columns in a file have all the values as NULL or missing, we discard such a file and move it to ["Bad_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Bad_Raw).
<br>
<br>
<br>
<br>

## Data Insertion in Database
### Here we have used Mongo DB for storing csv file
#### 1. Database Creation and connection - Create a database with the given name passed. If the database is already created, open the connection to the database. 
#### 2. Collection creation in the database - collection with name - "Good_Data", is created in the database for inserting the files in the "Good_Data_Folder" based on given column names and datatype in the schema file. If the collection is already present, then the new collection is not created and new files are inserted in the already present collection as we want training to be done on new as well as old training files.     
#### 3. Insertion of files in the collection - All the files in the ["Good_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Good_Raw) are inserted in the above-created table. If any file has invalid data type in any of the columns, the file is not loaded in the table and is moved to "Bad_Data_Folder".
#### Here is an Screen Shot
<p align="center">
<img src="https://github.com/rahulk15/images/blob/main/mongodb%20ss.png" alt="command">
</p>
<br>
<br>
<br>
<br>

## Model Training 
#### 1) Data Export from Mongo Db - The data in a stored database is exported as a CSV file to be used for model training.
#### 2) Data Preprocessing  
   #### a) Check for null values in the columns. If present, impute the null values using the KNN imputer
   #### b) transform the features using log transformation
   #### c) Scale the training and test data separately 
#### 3) Clustering - KMeans algorithm is used to create clusters in the preprocessed data. The optimum number of clusters is selected by plotting the elbow plot, and for the dynamic selection of the number of clusters, we are using "KneeLocator" function. The idea behind clustering is to implement different algorithms
 #### To train data in different clusters. The Kmeans model is trained over preprocessed data and the model is saved for further use in prediction.
#### 4) Model Selection - After clusters are created, we find the best model for each cluster. We are using two algorithms, "Random forest Regressor" and “Linear Regression”. For each cluster, both the algorithms are passed with the best parameters derived from GridSearch. We calculate the Rsquared scores for both models and select the model with the best score. Similarly, the model is selected for each cluster. All the models for every cluster are saved for use in prediction. 
<br>
<br>
<br>
<br>


## Prediction Data Description

#### Client will send the data in multiple set of files in batches at a given location. Data will contain climate indicators in 8 columns.
#### Apart from prediction files, we also require a "schema" file from client which contains all the relevant information about the training files such as:
- #### Name of the files, Length of Date value in FileName, Length of Time value in FileName, Number of Columns, Name of the Columns and their datatype.
- [Link for Schema file](https://github.com/rahulk15/cementStrengthPrediction/blob/main/schema_prediction.json)

<br>
<br>
<br>
<br>

## Data Validation1  
#### In this step, we perform different sets of validation on the given set of training files.  
#### 1) Name Validation- We validate the name of the files on the basis of given Name in the schema file. We have created a regex pattern as per the name given in schema file, to use for validation. After validating the pattern in the name, we check for length of date in the file name as well as length of time in the file name. If all the values are as per requirement, we move such files to ["Good_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Good_Raw) else we move such files to ["Bad_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Bad_Raw).
#### 2) Number of Columns - We validate the number of columns present in the files, if it doesn't match with the value given in the schema file then the file is moved to ["Bad_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Bad_Raw). 
#### 3) Name of Columns - The name of the columns is validated and should be same as given in the schema file. If not, then the file is moved to ["Bad_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Bad_Raw). 
#### 4) Datatype of columns - The datatype of columns is given in the schema file. This is validated when we insert the files into Database. If dataype is wrong then the file is moved to ["Bad_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Bad_Raw).. 
#### 5) Null values in columns - If any of the columns in a file has all the values as NULL or missing, we discard such file and move it to ["Bad_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Bad_Raw).  
<br>
<br>
<br>
<br>



## Data Insertion in Database1 
#### 1) Database Creation and connection - Create database with the given name passed. If the database is already created, open the connection to the database. 
#### 2) Table creation in the database - Table with name - "Good_Data", is created in the database for inserting the files in the "Good_Data_Folder" on the basis of given column names and datatype in the schema file. If table is already present then new table is not created, and new files are inserted the already present table as we want training to be done on new as well old training files.     
#### 3) Insertion of files in the table - All the files in the ["Good_Data_Folder"](https://github.com/rahulk15/cementStrengthPrediction/tree/main/Good_Raw) are inserted in the above-created table. If any file has invalid data type in any of the columns, the file is not loaded in the table and is moved to "Bad_Data_Folder".

<p align="center">
<img src="https://github.com/rahulk15/images/blob/main/cement%20predmongo%20ss.png" alt="command">
</p>
<br>
<br>
<br>
<br>



## Prediction 
 
#### 1) Data Export from Db - The data in the stored database is exported as a CSV file to be used for prediction.
#### 2) Data Preprocessing   
   #### a) Check for null values in the columns. If present, impute the null values using the KNN imputer
   #### b) transform the features using log transformation
   #### c) Scale the training and test data separately 
#### 3) Clustering - KMeans model created during training is loaded, and clusters for the preprocessed prediction data is predicted.
#### 4) Prediction - Based on the cluster number, the respective model is loaded and is used to predict the data for that cluster.
#### 5) Once the prediction is made for all the clusters, the predictions along with the original names before label encoder are saved in a CSV file at a given location and the location is returned to the client.
<p align="center">
<img src="https://github.com/rahulk15/images/blob/main/cement%20prediction.png" alt="command">
</p>
<br>
<br>
<br>
<br>

# Logging
## Training Logs
- Each and Every Step or every action it generartes logs and store it in Mongo DB. so we can know at what time which actions have done or where it is giving me an error.
<p align="center">
<img src="https://github.com/rahulk15/images/blob/main/cement%20training%20logs.png" alt="command">
</p>
- Fetch the data from mongo db
<br>
<br>
<br>
<br>
<br>

## Prediction Logs
- Each and Every Step or every action it generartes logs and store it in Mongo DB. so we can know at what time which actions have done or where it is giving me an error.
<p align="center">
<img src="https://github.com/rahulk15/images/blob/main/cement%20prediction%20logs.png" alt="command">
</p>
<br>
<br>
<br>
<br>
<br>



## Glimpse of Dataset
  <p align="center">
<img src="https://github.com/rahulk15/images/blob/main/Screenshot%202021-04-16%20223124.png" alt="command">
</p>

