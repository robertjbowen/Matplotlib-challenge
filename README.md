# Matplotlib-Challenge

This project was to manipulate Pandas Data Frames using Jupyter Notebook to download, clean, and analyze Pharmaceutical Study Data and create a series of different data plots and regression models.


### Documents in this repository are:

* pymaceuticals_Bowen.ipynb - My Jupyter Notebook file running a Python 3 kernel that contains all of the code for conducting the data analysis 

* data directory containing the source file of purchasing data - purchase_data.csv

* images folder - contains images of the code blocks and their outputs

* Checkpoints directory containing checkpoint .ipynb files


### Design concept:

The project begins with readng in two .csv files of study metadata and study results of the effects of different treatment regimens employed on laboratory mice over a fixed time period. The two data sets are merged into a single DataFrame (study_data). 

![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture1.png)

The study_data DataFrame is then scrubbed to identify and data rows that have duplicate time values for the same mouse ID. These rows are identified and all data pertaining to the specific mouse ID is removed from the data set. 

![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture2.png)

The resulting DateFrame is called (cleaned_data). A set of Summary Statistics is generated for the cleaned_data set using two methods. 

1. Using multiple groupby methods using the 'Drug Regimen' column to create a set of summary DataFrames for each calculation of mean, median, variance, standard deviation, and standard error of the mean. Then merging the DataFrames to create a single final DataFrame (summary_stats)

2. Using the groupby().agg method to generate the summary DataFrame (regimen_agg) in asigle line of code.

The results were identical DataFrames.

![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture3.png)

***
### Bar Charts:


The analysis consisted of generating a bar chart of total mice in the study for each of the drug regimens tested using the Pandas DataFrame.plot(kind="bar") method and the python plt.bar method. The first step was to remove all of the duplicate rows based on 'Mouse ID' to create a single row for each Mouse ID. The result was a DataFrame (regimen_mice) with 248 rows. The DataFrame was then grouped by 'Drug Regimen' to enable plotting versus the number of mice.

The results after formating were identical plots showing each drug regimen involved 24-25 mice.

![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture4_Pandas.png) ![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture5_Plot.png)

***
### Pie Charts:


The analysis consisted of generating a pie chart of Female versus Male Mice employed in the study using the Pandas DataFrame.plot(kind="pie") method and the python plt.pie method. The analysis started with the regimen_mice DataFrame from above but grouped by 'Sex' to enable plotting versus the number of mice.

The results after formating were identical plots showing 50.4% Male and 49.6% Female.

![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture6_Pandas.png) ![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture7_Pie.png)

***
### Quartiles, Outliers, and Box Plots:

The analysis consisted of calculating the final tumor volume of each mouse across four of the treatment regimens:  
* Capomulin
* Ramicane
* Infubinol
* Ceftamin

This was accomplished by grouping the cleaned_data DataFrame by 'Mouse ID' and filtering for the maximum value in the 'Timepoint' column for each mouse. The resulting DataFrame (time_max) was then merged with the original cleaned_data DataFrame using a left merge to just return the full data set for the max time rows for each mouse (mouse_max)

A for loop was then used to create a Series of the max tumor volumes for each treatment regimen (tumor_volume) which was then converted to a list (tumor_vol) and appended to a list (tumor_data). While in the loop, the quartiles, interquartile range and upper and lower bounds were calulated to determine if there are any potential outliers.

Infubinol has one potential outlier.

![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture8.png) 

A box plot of the Tumor Volumes across each of the four regimens was generated using the plt.boxplot method.

![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture9_Box.png)

***
### Line Plots:


The analysis consisted of creating a DataFrame of just the Capamulin Regimen data from the cleaned_data DataFrame (cap_data).

A single 'Mouse ID' was chosen from the set and a line plot of 'Tumor Volume vs. Time Point' was generated. The plot shows the tumor volume to be decreasing over time.

![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture10_Single.png)

I also generated a line plot of all 25 mice in the Capamulin data set. All but one mouse shows the tumor volumes decreasing by the end of the study, but one mouse showed an increase in volume.

![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture11_Multi.png)

***
### Scatter Plots and Linear Regression:


The final step in the analysis consisted of grouping the Capamulin DataFrame (cap_data) by Mouse ID and calulating the mean of the Tumor Volumes and Mouse Weights in order to generate a scatter plot of 'Average Tumor Volume vs. Mouse Weight for the Capomulin Regimen'.

![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture12_Scatter.png)

The plot shows a positive correlation based on the generally linear pattern from lower left to upper right. This was confirmed by calculating the correlation coefficient (0.84) and calculating a linear regression line.

![alt tag](https://github.com/robertjbowen/matplotlib-challenge/blob/main/images/Picture13_Regression.png)