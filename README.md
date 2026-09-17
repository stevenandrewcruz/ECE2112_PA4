# ECE2112_PA4
Written and made by Steven Andrew A. Cruz of 2ECE-D
# EXPERIMENT 4: DATA WRANGLING AND DATA VISUALIZATION 
In this experiment, the main topic revolves around organizing data and visualizing the data through a 2D image graph. The experiment includes filtering tabular data using several categorical and numerical conditions. To construct focused DataFrames by selecting relevant features. Summarize the relationship between categorical features and a numerical variable and communicate a data comparison using clear and correctly labeled plots.  

# IMPORT PANDAS AND MATPLOTLIB
```python
import pandas as pd 
import matplotlib.pyplot as plt 
```
Pandas and Matplotlib were imported at the start in order to make use of their respective syntax libraries. 

# A. VISAYAS COMMUNICATION DATAFRAME 
Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Track
is Communication. Retain only these columns, in the stated order: 'Name', 'Gender', 'Math', 'Electronics', 'Average'
Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to
the source dataset before the columns are selected.

Methods Used:
```python
board2= pd.read_excel('board2.xlsx')
```
To load the file `board2.xlsx` the function `pd.read_excel` was used in order to load the specific file type of board2 which is `xlsx`. This is stored in the Data Frame `board2`.

```python
board2['Average']=board2[['Math','Electronics','GEAS','Communication']].mean(axis=1)
board2
```
In this line of code, the `Average` column was computed for by getting the mean across the columns mainly for the 4 subjects for each individual row. The function `.mean(axis=1)` was used to calculate for the average of `['Math','Electronics','GEAS','Communication']` within `board2` as shown in the line of code. This is then stored in board2 under a new column `Average`. 

```python
VisComm = board2.loc[(board2['Hometown']=='Visayas')&(board2['Track']=='Communication'),['Name','Gender','Math','Electronics','Average'],]
VisComm
```
Within the data frame `VisComm` is the stored data for students whose Hometown is Visayas and their Track is Communication with their Names, Gender, and their data under Math, Electronics, and their Averages. The line of code uses the function `board2.loc` in order to find the students under Visayas and Communication with their respective data for the 5 specified columns.   

```python
print(f'Number of Rows: {len(VisComm)}')
display(VisComm)
```
This line of code displays both the contents of the data frame `VisComm` and prints the actual number of its rows with the use of the function `{len(VisComm)}` by measuring the number of rows within the data frame. The `f` function is used to help print the output `Number of Rows: 5`. 

# B. VISAYAS FEMALE DATAFRAME 
Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and
whose Gender is Female. Retain only: 'Name', 'Track', 'GEAS', 'Electronics', 'Average'
Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60. Do not
overwrite VisFemale when performing this second filter.

Methods Used: 

```python
VisFemale = board2.loc[(board2['Hometown']=='Visayas')&(board2['Gender']=='Female'),['Name','Track','GEAS','Electronics','Average'],]
VisFemale 
```
For this line of code, the data frame known as `VisFemale` has stored data containing specifically Females in Visayas with their Name, Track, and their data in GEAS, Electronics, and their Averages. Using the function `board2.loc` the specified conditions are done essentially locating the specified Hometown and Gender as well as the required columns and their data as shown in the line of code. 

```python
display(VisFemale)
display(VisFemale.loc[(VisFemale['Average']>=60)])
```
The first line of code displays the data in `VisFemale`, while the second line of code locates within the data frame averages greater than or equal to 60 with the use of the function `VisFemale.loc[(VisFemale['Average']>=60)]`.

# C. CATEGORY-AVERAGE VISUALIZATION 
Examine how the recorded Average differs across the three categorical features Track, Gender, and
Hometown.
a. For each feature, compute the mean of Average for every category using Pandas.
b. Display the three summary tables.
c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by
Hometown.
d. Below the figure, write three concise statements identifying the category with the highest sample
mean for each feature.
Interpretation rule: Describe the observed dataset only. A difference in group means does not, by
itself, establish that a feature causes a higher board-exam score.

Methods Used: 

```python
track_mean = board2.groupby('Track')['Average'].mean().reset_index()
gender_mean = board2.groupby('Gender')['Average'].mean().reset_index()
hometown_mean = board2.groupby('Hometown')['Average'].mean().reset_index()

display(track_mean)
display(gender_mean)
display(hometown_mean)
```
There are 3 data frames named track_mean, gender_mean, and hometown_mean. The function `board2.groupby('')[''].mean().reset_index()` basically groups the 3 specified columns with their respective averages and computes their respective mean from their averages. 

```python
fig, axes = plt.subplots(1,3, figsize=(18,5))
```
This line of code `fig, axes = plt.subplots(1,3)` essentially sets the subplots stating how many rows (1) and how many columns (3) are needed, which results to 3 graphs in 1 row. The syntax `axes[]` uses a standard Python list indexing wherein it targets and modify a specific subplot within a multi-plot Matplotlib figure. The indexes `0,1,2` represents the subplots or graphs from left to right with `0` being the starting plot from the left. 

```python
axes[0].bar(track_mean['Track'], track_mean['Average'], color='skyblue',edgecolor='black')
axes[0].set_title('Mean Average by Track')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Mean Average')
axes[0].set_ylim(0,80)

axes[1].bar(gender_mean['Gender'], gender_mean['Average'], color='purple',edgecolor='black')
axes[1].set_title('Mean Average by Gender')
axes[1].set_xlabel('Gender')
axes[1].set_ylabel('Mean Average')
axes[1].set_ylim(0,80)

axes[2].bar(hometown_mean['Hometown'], hometown_mean['Average'], color='red',edgecolor='black')
axes[2].set_title('Mean Average by Hometown')
axes[2].set_xlabel('Hometown')
axes[2].set_ylabel('Mean Average')
axes[2].set_ylim(0,80)
```

The function `.bar()` is where the data from the 3 data frames created can be displayed through a 2D bar image. Using this line of code `axes[0].bar(track_mean['Track'], track_mean['Average'],color='skyblue',edgecolor='black')` as an example, it is used to shape the bar of that specific graph. Using the data from `track_mean` and calling its 2 columns; `Track` and `Average` the data from the data frame is applied and displayed through a bar in the graph. Its appearance can be manipulated with `color='skyblue',edgecolor='black'` changing the color of the bar. 

The functions `.set_title`, `.set_xlabel`, and `.set_ylable` are used to name the graphs. Using these lines of code `axes[0].set_title('Mean Average by Track'), axes[0].set_xlabel('Track'), axes[0].set_ylabel('Mean Average')` as examples, the `.set_title` is used to name the first graph with `Mean Average by Track`. This can be seen at the top of that specific graph, while `.set_xlabel('Track')` gives the x-axis the name `Track`, and `.set_ylabel('Mean Average')` gives the y-axis the name `Mean Average`. Finally, the function `.set_ylim(0,80)` is used to set the parameter of the bar graphs. It limits the y-axis values to only `80` to better see the differences between the data within each graphs. 

```python
fig.text(0.125,-0.1,'Interpretation:', weight='bold',size=13)
fig.text(0.125,-0.25, 'The figure for Track, shows Communication to have the highst mean of (67.975).\n'
           'The figure for Gender, shows Male to have highest mean of (67.183333).\n'
           'The figure for Hometown, shows Luzon to have the highest mean of (68.083333).\n', size=11)

plt.show()
```
In order to display the interpretation of the graph the function `fig.text()` was used. This function is used twice containing `0.125,-0.1,'Interpretation:', weight='bold',size=13` for the first and the second contains different coordinates `0.125,-0.25` with the actual interpretation of the graph. These coordinates specifically places them both beneath the row of the 3 graphs. As seen on the line of code the `Interpretation` is located slightly above the the actual interpretation of the graph. The interpretation states the highest mean for each graph. The line of code at the very bottom `plt.show` essentially displays all currently created Matplotlib figures on the screen.  


README HISTORY:
- September 13 2026 Repository creation 
- September 13 2026 Uploaded Jupyter notebook and board2. xlsx file
- September 17 2026 Layout of Readme file 
- September 17 2026 Finalizing of Readme file
- September 18 2026 Minor editing 




