# Data-Cleaning-Preprocessing-for-ML-

1) To overcome the issues related to the read ".xlsx" file can be solved by upgrading the pandas. 
<img width="906" alt="Screenshot 2022-12-31 at 11 54 45" src="https://user-images.githubusercontent.com/64656686/210127473-bc72831b-49d6-4705-b438-1b136a43775c.png">

2) Read the data file (which is included here) using the pandas.read_excel() as df. Then use df.head() to check first 5 rows of the data frames. df.shape() uses to check the size (rows*columns) of the data frame. 
<img width="906" alt="Screenshot 2022-12-31 at 12 07 30" src="https://user-images.githubusercontent.com/64656686/210127749-e9e14459-bd38-4e30-b8be-42029f6285e6.png">

# Data quality checking

3) To get the information about the stored data based on columnwise it can use df.info()
<img width="898" alt="Screenshot 2022-12-31 at 12 09 29" src="https://user-images.githubusercontent.com/64656686/210127803-c9b24060-efaf-4e71-9964-b3b1046cc8b4.png">
Note - Some data like "date" should be stored under the Date and Time data types, "age" must be int64 data type. Likewise there are issues with the data type which need to be addressed. 


4) Check the data anomalies by using the the df[''].unique(), unique() function and the number of unique object by nunique() funtion
<img width="901" alt="Screenshot 2022-12-31 at 12 19 33" src="https://user-images.githubusercontent.com/64656686/210128039-7dd09385-b345-48a6-b377-80741a46cf06.png">
Ex- object us and usa both reffers to the same country, we should avoid these kind of anomalies by checking the others columns also. 


5) Check the missing values of the each columns of the data frame by using the df.isna().sum(). Here it sum up every missing values to the each column by using the sum() function
<img width="921" alt="Screenshot 2022-12-31 at 12 27 54" src="https://user-images.githubusercontent.com/64656686/210128257-dcc11bb1-d3a4-45e8-9f82-8572040d83de.png">
Sometimes haiving very small amount of missing values might be not a harmful damage to the prediction values. But we can't decide it by checking only the num of missing values of the each columns. To get and clear idea,  we can use (df.isna().sum()*100)/len(df) to get the precentage of missing values of the each columns. 
<img width="909" alt="Screenshot 2022-12-31 at 12 36 06" src="https://user-images.githubusercontent.com/64656686/210128457-9dae6e8f-2c40-4405-8769-0b0b09f96c4e.png">

6) Check the duplicated values of the data frame by using the df.duplicated()method. As it want to check the duplicated values based on columns it can use df[df.duplicated()]. 
<img width="920" alt="Screenshot 2022-12-31 at 12 49 33" src="https://user-images.githubusercontent.com/64656686/210128793-1b585dc5-06f9-448e-9f32-590de39a56ef.png">
Here is no any duplication values in the data sets relates to each columns. 

# Data cleaning and preprocessing 

7) Replace error values with null values using pd.replace("ERR", np.nan)
<img width="921" alt="Screenshot 2022-12-31 at 15 00 10" src="https://user-images.githubusercontent.com/64656686/210131858-be0051d5-8c51-4b39-a808-c297865bb17f.png">
Ex- It needs to be converted the "ERR" values in the age column to null values. 
<img width="930" alt="Screenshot 2022-12-31 at 15 01 41" src="https://user-images.githubusercontent.com/64656686/210131890-0aeac662-618a-4477-be2c-b6552e5e940f.png">

8) Remove the missing values. 

Method 01 (For numeric data)

Here it is very easy to remove the rows with missing values to get a clear dataset but having large number of missing values can be leaded to reduce more rows and in the end it will lead to reduce machine learning model performances. So one way to to address this trade-off is to replace the missing values with the average values if the data type is integer. 

It can accomplish by following the below steps 

from sklearn.impute import SimpleImputer

imputer = SimpleImputer(missing_values=np.nan, strategy="mean")
  
df[['value', 'item purchased','monthly visits']] = imputer.fit_transform(df[['value', 'item purchased','monthly visits']])  
 
<img width="913" alt="Screenshot 2022-12-31 at 15 26 18" src="https://user-images.githubusercontent.com/64656686/210132507-2a365fbd-f1fb-45c9-a5b7-36215e460af0.png">

Method 2 

In this method, it is going to delete the rows with "Nan" values by using the df.dropna(inplace=True"). It uses inplace=True attribute to denote that deletion part is going to do for the loaded data set for permanently. 
<img width="915" alt="Screenshot 2022-12-31 at 15 36 09" src="https://user-images.githubusercontent.com/64656686/210132771-cb622875-66fd-4b6b-ae79-4b1052213851.png">

9) Removing white spaces. There might be some chances to include white spaces when entering data. For an example here when it entering the country some one mistakely can enter the "USA" as " USA" so it needs to check the clumns which can affected by the white spaces and need to reduce those things. 
<img width="913" alt="Screenshot 2022-12-31 at 15 47 50" src="https://user-images.githubusercontent.com/64656686/210133055-dbe75e9c-6168-472b-a22a-cc9d0c01e87a.png">

10) Work with the "data" column. First it needs to check the data type the of the "date" column by using the df.info() method. If it is not date time it needs to be converted to the datetime data type with the required date and time format. 

Check the current data type. 
<img width="928" alt="Screenshot 2022-12-31 at 16 00 15" src="https://user-images.githubusercontent.com/64656686/210133499-00e760d5-236f-46dd-a6d8-5536a30e86f7.png">

"date" column need to be convert to the "datetime" data format. 
df['date']=pd.to_datetime(df['date'],('if it rquires it can denote the datetime format here. ')) 
<img width="942" alt="Screenshot 2022-12-31 at 16 02 23" src="https://user-images.githubusercontent.com/64656686/210133564-1b43fbf8-6a5c-4db5-92dd-7d45bce427d6.png">

11) Converte the age date type float to integer data type.
<img width="921" alt="Screenshot 2022-12-31 at 21 02 07" src="https://user-images.githubusercontent.com/64656686/210144324-20afe988-52e1-47df-adb2-0a589700e4e5.png">

12) Remove data anomalies 

First it needs to check the is there any noticiable data anomaly issues. 
df.head(10)
<img width="937" alt="Screenshot 2022-12-31 at 21 09 27" src="https://user-images.githubusercontent.com/64656686/210147248-282f3e85-83a3-48cb-b5c2-4c3c23490bc8.png">
To check the anomalies clearly we can use df['country'].unique() method. 
<img width="918" alt="Screenshot 2022-12-31 at 21 11 40" src="https://user-images.githubusercontent.com/64656686/210148097-da868d1d-7e4d-47c8-a371-a108e3f7d87c.png">
Note - Here "USA" and "US" both reffers to the same country. So we can use one word to denote it. 

df['country']=df['country'].replace("USA", "US") can be used to replace the word to one commom word. 
<img width="919" alt="Screenshot 2022-12-31 at 21 13 21" src="https://user-images.githubusercontent.com/64656686/210148533-e7f3c4a1-ce89-4b40-bc4c-d6d50a2553d7.png">

13) Mapping catogerical values to numeric values 
In ML thee are some insidents where it requires to convert the catergorical varibles to the numeric variables. Here in example dat set it is goig to convert the 'gender' column to the numneric values by using the df['gender']=df['gender'].map({'Male':0, 'Female':1}). It has used the python dictionary inside the map function to denote the data which are required to convert into the numerics. 
<img width="917" alt="Screenshot 2022-12-31 at 21 22 36" src="https://user-images.githubusercontent.com/64656686/210148829-6e574e7a-c3c1-48d3-834a-8af28d45e5ac.png">

14)



















































