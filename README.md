# ADVANCED PROGRAMMING: Programming Assignment #4

## Project Overview  
This project contains solutions to data wrangling and data visualization problems using the Pandas and Matplotlib libraries as part of Advanced Programming Experiment 4. It demonstrates how to filter and subset data, create new calculated columns, and generate charts to analyze data.

## Project Significance
Using Pandas and Matplotlib allows data to be cleaned, filtered, and visualized quickly. Instead of manually checking exam results, we can use code to automate the process of identifying students that meet certain conditions, calculate averages, and create visual summaries.

## Getting Started
The code can be run in any Python environment or IDE. For this project, Jupyter Notebook was used through Anaconda Navigator to write and execute the solutions.

The dataset used in this assignment (board2.xlsx) was provided through the experiment instructions.
For convenience, the same Excel file is uploaded in this GitHub repository alongside the Jupyter Notebook, so that users can run the code directly.

Note: When opening Excel files directly in GitHub, the preview may look different compared to how it appears in Pandas or Excel. Always load the dataset into Pandas or Excel to view it correctly.

## Problems and Solutions

### 1. Instru DataFrame
- **Goal:** reate a DataFrame named Instru containing students who are from Instrumentation track, with Luzon as their hometown, and an Electronics grade greater than 70. Keep only the columns Name, GEAS, and Electronics.

- **Code:**  Import the Pandas library and use the **pd.read_csv( )** function to load the CSV file into a DataFrame named cars. To display the first five rows, call the **.head( )** method, and to display the last five rows, call the **.tail( )** method.
  ```python
  import pandas as pd
  df = pd.read_excel("board2.xlsx")

  Instru = df[(df["Track"] == "Instrumentation") &                                # filter Instrumentation track (constant 1)
            (df["Hometown"] == "Luzon") &                                       # filter Luzon hometown (constant 2)
            (df["Electronics"] > 70)]                                           # filter Electronics grade > 70
  Instru = Instru[["Name", "GEAS", "Electronics"]]                                # from the filtered, display their "Name", "GEAS", "Electronics" 
  Instru
  
- **Output:**
[Cars Head Output](FirstFive.png)

b.
```python
   cars.tail()
```
- **Output:**
[Cars Tail Output](LastFive.png)
      

 ### 2. Data Subsetting and Indexing Problem 
- **Goal:** Using the dataframe cars in problem 1, extract the following information using subsetting, slicing and indexing operations.
  - a. Display the first five rows with odd-numbered columns (columns 1, 3, 5, 7...) of cars.
  - b. Display the row that contains the ‘Model’ of ‘Mazda RX4’.
  - c. How many cylinders (‘cyl’) does the car model ‘Camaro Z28’ have?
  - d. Determine how many cylinders (‘cyl’) and what gear type (‘gear’) do the car models ‘Mazda RX4 Wag’, ‘Ford Pantera L’ and ‘Honda Civic’ have.

- **Code:** Begin by loading the CSV file into a DataFrame named cars using the **pd.read_csv( )** function. Use the **.loc[ ]** method to filter rows and select specific columns based on conditions. For Problem a, store the result in a variable called **FirstFive_odd**, which contains the first five rows with the odd-numbered columns explicitly listed. For Problem b, apply a condition to select the row with the model 'Mazda RX4'. For Problem c, filter the DataFrame to select only the cyl column for the model 'Camaro Z28'. For Problem d, run separate **.loc[ ]** commands for each model (Mazda RX4 Wag, Ford Pantera L, and Honda Civic) to display their corresponding cyl and gear values. An alternative approach is to use the **.isin( )** function to combine all three conditions in one run. However, note that when **.isin( )** is used, the results are automatically sorted according to the DataFrame’s index values, so although the instructions list Honda Civic last, it appears in the middle of the output because its index (18) comes after Mazda RX4 Wag (1) and before Ford Pantera L (28).

a.
  ```python
   import pandas as pd
    cars = pd.read_csv('cars.csv')
  FirstFive_odd = cars.loc[[0,1,2,3,4],['Model', 'cyl', 'hp', 'wt', 'vs', 'gear']]
  FirstFive_odd
  ```
  - **Output:**
[Problem 2A Output](Problem2A.png)

b.
  ```python
   cars.loc[cars['Model']=='Mazda RX4']
  ```
  - **Output:**
 [Problem 2B Output](Problem2B.png)

c.
  ```python
   cars.loc[(cars['Model']=='Camaro Z28'), ['cyl']]
  ```
  - **Output:**
 [Problem 2C Output](Problem2C.png)
  
d.
  ```python
   cars.loc[cars['Model'].isin(['Mazda RX4 Wag', 'Ford Pantera L', 'Honda Civic']), ['cyl', 'gear']]
  ```
  - **Output:**
 [Problem 2D Output](Problem2D.png)

