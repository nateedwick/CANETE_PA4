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

- **Code:**  Import the Pandas library and use pd.read_excel() to load the dataset into a DataFrame. Apply boolean conditions (Track = Instrumentation, Hometown = Luzon, Electronics > 70) to filter rows. Store the result in Instru. In a second step, select only the required columns (Name, GEAS, Electronics) from the filtered DataFrame. This “double-step” approach makes the filtering and column selection easier to read.
  
  ```python
  import pandas as pd
  df = pd.read_excel("board2.xlsx")

  Instru = df[(df["Track"] == "Instrumentation") &                                # filter Instrumentation track (constant 1)
            (df["Hometown"] == "Luzon") &                                       # filter Luzon hometown (constant 2)
            (df["Electronics"] > 70)]                                           # filter Electronics grade > 70
  Instru = Instru[["Name", "GEAS", "Electronics"]]                                # from the filtered, display their "Name", "GEAS", "Electronics" 
  Instru
  
- **Output:**
[Instru Output](dataframea.png)

 ### 2. Mindy DataFrame
- **Goal:** Create a DataFrame named Mindy containing students who are Female, from Mindanao, and have an Average grade of at least 55. Keep only the columns Name, Track, Electronics, and Average.

- **Code:** First, compute the Average column by taking the mean of the four subject columns (Math, Electronics, GEAS, Communication) per row. This ensures each student’s overall performance is available in a single column. Then apply boolean conditions (Hometown = Mindanao, Gender = Female, Average >= 55) to filter rows. Store the result in Mindy. In a second step, select only the required columns (Name, Track, Electronics, Average).
  
```python
 df["Average"] = df[["Math", "Electronics", "GEAS", "Communication"]].mean(axis=1)    # Create "Average" column = mean of Math, Electronics, GEAS, Communication
                                                                                     # .mean axis = 1, kasi row wise = avg. per students
Mindy = df[(df["Hometown"] == "Mindanao") &                                          # filter Mindanao hometown (constant 1)
           (df["Gender"] == "Female") &                                              # filter Female gender (constant 2)
           (df["Average"] >= 55)]                                                    # filter Average >= 55
Mindy = Mindy[["Name", "Track", "Electronics", "Average"]]                           # from the filtered, display their "Name", "Track", "Electronics", "Average"
Mindy
  ```
  - **Output:**
[Mindy Output](dataframeb.png)


