# Energy Data Analysis Project

![Project Banner](https://raw.githubusercontent.com/ShreyasLengade/Github-Images/main/Banner%20for%20DM%20project.webp)

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Datasets](#datasets)
  - [energy_dataset.csv](#energydatasetcsv)
  - [df_combined.csv](#dfcombinedcsv)
  - [Maximum_Load_Per_Day_with_Timestamps.csv](#maximumloadperdaywithtimestampscsv)
- [Exploratory Analysis and Data Cleaning](#exploratory-analysis-and-data-cleaning)
- [Handling Missing and Duplicate Values](#handling-missing-and-duplicate-values)
- [Modelling Process](#modelling-process)
- [Examples](#examples)

## Introduction

Welcome to the Energy Data Analysis Project! The project was developed to provide policy recommendation for renewable energy sources usage and infrastructure implementation by analysing the consumption patterns of existing sources in Valencia, Spain. This was achieved by forecasting the consumption of renewable resources through analysis of various energy datasets. Visualisation, trends and meaningful insights are provided.

## Features

- **Data Preprocessing**: Clean and prepare data for analysis.
- **Exploratory Analysis**: Investigate data distributions and characteristics.
- **Visualization**: Generate various plots to visualize energy consumption trends.
- **Analysis**: Detailed analysis of energy data including maximum load per day with timestamps.
- **Forecasting**: Predict future energy consumption using advanced models.
- **Reports**: Generate comprehensive reports based on the analysis.

## Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/ShreyasLengade/Energy-Consumption-Forecasting.git
    ```

2. Navigate to the project directory:
    ```bash
    cd Energy-Consumption-Forecasting
    ```

3. Install the required dependencies:
    ```bash
    pip install -r requirements.txt
    ```

## Usage

To run the analysis, open the `main.ipynb` notebook and execute the cells. Make sure all the datasets are in the correct directory. You'll get the in-depth explanations as a comment under each analysis and visaulisation as well in this file.

## Datasets

### energy_dataset.csv

This dataset contains detailed information on energy consumption patterns. It includes various features such as timestamps, energy loads, and more.

### df_combined.csv

This dataset is a combination of multiple sources, providing a comprehensive view of energy data over a specific period.

### Maximum_Load_Per_Day_with_Timestamps.csv

This dataset includes the maximum energy load per day along with their respective timestamps, which helps in identifying peak consumption times.

## Exploratory Analysis and Data Cleaning

For exploratory analysis and data cleaning of all the data generation sources in Valencia, we used the violin plot to see the distribution of values. Then we used the `.info()` method to investigate the type of values and the count of null and non-null values of these sources. 

Next, we decided to drop the "Price" column. The rationale behind this decision is: 

"As we have a lot of data columns, we will take only the relevant columns required for our model. Keep in mind 'price' is an important column, but we also require 'Appliances' data that can be used for the forecasting model. As we don't have 'Appliances' data, we will not consider the 'Price' column data for our model."

## Handling Missing and Duplicate Values

### Duplicate Values

"As we can see, the 'energy_df' dataframe has no duplicate values. Nevertheless, it has some NaNs, and thus, we have to investigate further. Since this is a time-series forecasting task, we cannot simply drop the rows with the missing values, and it would be a better idea to fill the missing values using interpolation."

### Missing Values

"Most null values can be found in the 'total load actual' column, which represents energy consumption. Therefore, it is a good idea to visualize it and see what we can do. The similar numbers in null values in the columns related to the type of energy generation probably indicate that they will also appear in the same rows. Let us first define a normal distribution to see the irregularities."

"After zooming into the first 2 weeks of the 'total load actual' column, we can already see that there are null values for a few hours. However, the number of missing values and the behavior of the series indicate that an interpolation would fill the NaNs quite well. Let us further investigate if the null values coincide across the different columns. Let us display the last five rows."

"If we manually searched through all of them, we would confirm that the null values in the columns related to the type of energy generation mostly coincide. The null values in 'actual total load' also coincide with the aforementioned columns, but also appear in other rows as well. In order to handle the null values in 'df_energy', we will use a linear interpolation with a forward direction. Perhaps other kinds of interpolation would be better; nevertheless, we prefer to use the simplest model possible. Only a small part of our input data will be noisy, and it will not affect performance noticeably."

"As we can see the count of values of all columns is similar, so now let us see through the line plot again."

## Modelling Process

"Now let us start the modelling process. We tried multiple models like ARIMA, Auto-ARIMA, SARIMAX, Prophet, XGBoost, and RFR. Finally, we proceeded with XGBoost and RFR."

"Looking into the R^2 value, our model seems to be perfectly fit, but we want to add another additional requirement for our stakeholder in which we want to forecast the maximum energy consumption for each day according to the 'total load actual' column's maximum value for each day. For this, we have filtered out data through Excel, where we have taken the maximum values of the 'total load actual' column for each day for the corresponding 'time' column."

## Examples

Below are some examples of the visualizations and analysis you can perform with this project:

1. **Energy Load Over Time**
    ```python
    import matplotlib.pyplot as plt
    import pandas as pd

    df = pd.read_csv('energy_dataset.csv')
    df.plot(x='timestamp', y='load', title='Energy Load Over Time')
    plt.show()
    ```

2. **Maximum Load Per Day**
    ```python
    df_max_load = pd.read_csv('Maximum_Load_Per_Day_with_Timestamps.csv')
    df_max_load.plot(x='date', y='max_load', kind='bar', title='Maximum Load Per Day')
    plt.show()
    ```

---

Thank you for checking out our project! If you find it useful, please give it a star ⭐ on GitHub.


