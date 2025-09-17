# Programming Assignment 2 – Data Wrangling and Visualization

**Author:** SAEZ, Eljenzal Hoper U.  
**Course:** Advanced Computer Programming and Algorithms / ECE2112

---

## 📌 Description

This Jupyter Notebook presents solutions to a data-driven storytelling task focused on data wrangling and data visualization using Python and Pandas. The experiment explores how structured data can be cleaned, filtered, and visualized to reveal meaningful insights—especially in the context of academic performance.

Key objectives include:
- Constructing multiple filtered DataFrames based on conditions like track, gender, hometown, and subject scores
- Applying logical indexing and conditional selection to extract relevant subsets
- Visualizing how features such as track, gender, and hometown influence average grades
- Saving processed data for reproducibility and future analysis

This task emphasizes the power of data visualization — turning raw exam data into structured insights that can inform decisions and highlight trends.

## ⚙️ Requirements
- Python 3.x (Recommended version: 3.8 or higher)
- Jupyter Notebook
- Numpy
- Pandas 
- Matplotlib (for basic plotting)
- Seaborn (for enhanced statistical visualizations)

---

## ▶️ How to Run

1. Install [Jupyter Notebook](https://jupyter.org/install) if not already installed.  
2. Open the notebook file: EXPERIMENT_4_DataWrangling_Visualization.ipynb
3. Run each cell one by one to see the results.
4. Check the tables and graphs shown in the notebook.
5. Look in the folder for any saved files like charts or cleaned data.

## 💡 Code Explanation

### 01.a ECE BOARD EXAM PROBLEM

```python
# DataFrame Representation

instru = pd.DataFrame(boards, columns=['Name','GEAS','Electronics','Track','Hometown']) # set the data frame in order for it to only show Name, Geas, Electronics
# Track and Hometown will be filtered out later since they're constant

x = instru.loc[(instru['Electronics'] > 70) & (instru['Hometown']=='Luzon') & (instru['Track']=='Instrumentation'), ['Name','GEAS','Electronics']] # use .loc to find the Electronics column to be > 70, 
# find Hometown which is equal to Luzon, and Track which is equal to Instrumentation
# only show Name, GEAS, and Electronics in DataFrame set.

x

```

```python
instru = pd.DataFrame(boards, columns=['Name','GEAS','Electronics','Track','Hometown'])
```
- Creates a new DataFrame named instru from the existing data boards.

```python
x = instru.loc[
    (instru['Electronics'] > 70) &
    (instru['Hometown'] == 'Luzon') &
    (instru['Track'] == 'Instrumentation'),
    ['Name','GEAS','Electronics']
]
```

- Filters the instru DataFrame to find specific students based on three conditions.

 - Condition 1: instru['Electronics'] > 70 → selects students with Electronics scores above 70.

 - Condition 2: instru['Hometown'] == 'Luzon' → limits results to students from Luzon.

 - Condition 3: instru['Track'] == 'Instrumentation' → focuses only on those in the Instrumentation track.

 - Final Output Columns: Only shows 'Name', 'GEAS', and 'Electronics' in the result.


### 01.b ECE BOARD EXAM PROBLEM

```python
Mindy = pd.DataFrame(boards, columns=['Name','Gender','Track','Math','Electronics','GEAS','Communication','Hometown']) # set the data frame in order for it to only show Name, Track, Electronics
# Hometown and Gender  will be filtered out later since they're constant

Mindy['Average'] = Mindy[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1) # make a new column with the mean of Math, Electronics, GEAS, and Communication in each row.

Mindydata = Mindy.loc[(Mindy['Average'] >= 55) & 
        (Mindy['Hometown']=='Mindanao') & 
        (Mindy['Gender']=='Female'), 
        ['Name','Track','Electronics','Average']] # use .loc so that it will only show the specific parameters needed.

Mindydata
```

```python
Mindy = pd.DataFrame(boards, columns=['Name','Gender','Track','Math','Electronics','GEAS','Communication','Hometown'])
```
- Creates a new DataFrame named Mindy from the original dataset boards.

```python
Mindy['Average'] = Mindy[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
```
- Adds a new column called 'Average' to the Mindy DataFrame.

```python
Mindydata = Mindy.loc[
    (Mindy['Average'] >= 55) &
    (Mindy['Hometown'] == 'Mindanao') &
    (Mindy['Gender'] == 'Female'),
    ['Name','Track','Electronics','Average']
]
```
- Filters the Mindy DataFrame to find specific students based on three conditions.

 - Condition 1: Average >= 55 → selects students with solid overall performance.

 - Condition 2: Hometown == 'Mindanao' → focuses on students from Mindanao.

 - Condition 3: Gender == 'Female' → limits results to female students.

 - Final Output Columns: Displays only 'Name', 'Track', 'Electronics', and 'Average'.



### 02 ECE BOARD EXAM PROBLEM VISUALIZATION

```python
gender = Mindy.groupby('Gender')['Average'].mean()
track = Mindy.groupby('Track')['Average'].mean()
hometown = Mindy.groupby('Hometown')['Average'].mean()

plt.figure(figsize=(12, 6)) # resize the bar graph to make it readable

bars = plt.bar(['Male', 'Female', 'Instrumentation', 'Communication', 'Microelectronic', 'Luzon', 'Visayas', 'Mindanao'], list(gender.values)+list(track.values)+list(hometown.values))
#  makes a bar graph, the x labels the combination of categories, and y labels the the average scores.

plt.xlabel('Categories') # add x label as categories
plt.ylabel('Average Score') # add y label as average score
plt.title('Graph for Tracks, Gender, and Hometown') # add title as graph for tracks, gender, and hometown

# show the plot
plt.tight_layout()
plt.show()
```


```python
gender = Mindy.groupby('Gender')['Average'].mean()
track = Mindy.groupby('Track')['Average'].mean()
hometown = Mindy.groupby('Hometown')['Average'].mean()
```

- Calculate the average score for each gender.
- Compute the average score for each academic track.
- Find the average score for each hometown region.

```python
plt.figure(figsize=(12, 6))

```
- Set up the plot canvas size

```python
bars = plt.bar(
    ['Male', 'Female', 'Instrumentation', 'Communication', 'Microelectronic', 'Luzon', 'Visayas', 'Mindanao'],
    list(gender.values) + list(track.values) + list(hometown.values)
```

- Draw the bar chart combining three category sets.
- The x-axis labels are a single list of all category names: genders, tracks, and hometowns.
- The y-axis heights are the corresponding mean values from gender, track, and hometown.

##### *- 🌱“Failure is not the opposite of success; it’s part of success.”*

### 📝 Commitments

- **v1.0** – Initial draft
 - Loaded and cleaned the dataset
 - Built initial filtered DataFrames

- **v1.1** – Rechecking
 - Calculated average scores and created the combined bar chart
  
- **v1.2** – Final polish
 - Added clear explanations and finalized the README layout

 ---






