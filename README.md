# Data-Cleaning-Preprocessing-for-ML-

1) To overcome the issues related to the read ".xlsx" file can be solved by upgrading the pandas. 
<img width="906" alt="Screenshot 2022-12-31 at 11 54 45" src="https://user-images.githubusercontent.com/64656686/210127473-bc72831b-49d6-4705-b438-1b136a43775c.png">

2) Read the data file (which is included here) using the pandas.read_excel() as df. Then use df.head() to check first 5 rows of the data frames. df.shape() uses to check the size (rows*columns) of the data frame. 
<img width="906" alt="Screenshot 2022-12-31 at 12 07 30" src="https://user-images.githubusercontent.com/64656686/210127749-e9e14459-bd38-4e30-b8be-42029f6285e6.png">

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


