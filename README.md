# ADVANCED PROGRAMMING: Programming Assignment #4

## Project Overview  
This project contains solutions to data wrangling and data visualization problems using the Pandas and Matplotlib libraries as part of Advanced Programming Experiment 4. It demonstrates how to filter and subset data, create new calculated columns, and generate charts to analyze data.

## Project Significance
Using Pandas and Matplotlib allows data to be cleaned, filtered, and visualized quickly. Instead of manually checking exam results, we can use code to automate the process of identifying students that meet certain conditions, calculate averages, and create visual summaries.

## Getting Started
The code can be run in any Python environment or IDE. For this project, Jupyter Notebook was used through Anaconda Navigator to write and execute the solutions.

The dataset used in this assignment (board2.xlsx) was provided through the experiment instructions.
For convenience, the same Excel file is uploaded in this GitHub repository alongside the Jupyter Notebook, so that users can run the code directly.

Note: When opening Excel files directly in GitHub, the preview may look different compared to how it appears in Pandas or Excel. Always load the dataset into Pandas or Excel to view it correctly. Also make sure that the Jupyter Notebook file (.ipynb) and the Excel dataset (board2.xlsx) are stored in the same folder. Otherwise, the pd.read_excel("board2.xlsx") command will not work because Python will not be able to locate the file.

## Problems and Solutions

### 1. Instru DataFrame
- **Goal:** Create a DataFrame named Instru containing students who are from Instrumentation track, with Luzon as their hometown, and an Electronics grade greater than 70. Keep only the columns Name, GEAS, and Electronics.

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

### 3. Visualization – Average Scores
- **Goal:** Create a visualization that shows how the different features contributes to average grade

- **Code:** Begin by importing the Matplotlib library using import matplotlib.pyplot as plt.
Then, for each factor (Track, Gender, Hometown), use the Pandas groupby() function to group the dataset by that factor and compute the mean of the Average column using .mean(). After grouping, call .plot(kind="bar") on the result to generate a bar chart. Add a title with plt.title(), a y-axis label with plt.ylabel(), and finally call plt.show() to display the graph. Repeat this process separately for Track, Gender, and Hometown, resulting in three bar charts.
  
```python
 import matplotlib.pyplot as plt
df.groupby("Track")["Average"].mean().plot(kind="bar")                                # bar graph of average score by Track
plt.title("Average Score by Track")
plt.ylabel("Average Grade")
plt.show()
  ```
  - **Output:**
[Average Score by Track](visualization1.png)

```python
 df.groupby("Gender")["Average"].mean().plot(kind="bar")                               # bar graph of average score by Gender
plt.title("Average Score by Gender")
plt.ylabel("Average Grade")
plt.show()
  ```
  - **Output:**
[Average Score by Gender](visualization2.png)

```python
 df.groupby("Hometown")["Average"].mean().plot(kind="bar")                              # bar graph of average score by Hometown
plt.title("Average Score by Hometown")
plt.ylabel("Average Grade")
plt.show()
  ```
  - **Output:**
[Average Score by Hometown](visualization3.png)
