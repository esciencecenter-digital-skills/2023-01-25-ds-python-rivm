---
layout: page
title: "Guided version of the post-workshop exercise"
---

# Guided version post-workshop exercise
**This is a guided version of the post-workshop exercise, please read the [the open version](./post-workshop-exercise.html) first!**

## 0. Loading, cleaning, and selecting the data
Before you can solve any of the questions, you first need to load and clean the dataset. 
And select the right data. What follows are 
questions that help you with this, step by step, without providing the answers.

### 0.1 Loading the data
1. Load the data into Python with pandas. (Hint: check the separator that is used in the file, you can pass a different separator to `read_csv()` using the `sep` argument)
2. Take a look at the data. As you can see, the Topic is read as a column and not as index. You can fix this by passing `index_col='Topic'` to `read_csv()`.

### 0.2 Cleaning up the data
1. Take a look at the data. How are missing data represented?
2. Replace the value that is used for missing data with NaN. (hint: You can replace values using DataFrame.replace(). You can use `numpy.nan` to represent NaN values. NumPy is the fundamental package for scientific computing with Python, it operates a lot on the background of Pandas, but in this case we will import it. This is usually done like this: `import numpy as np`)
3. Rename the 'Unnamed: 1' column to 'unit'
4. What is the datatype of the numerical values?
5. Convert all data in the numerical columns (all columns excluding 'unit') to the 'float' datatype. Use a for-loop to loop over all the numerical columns. Change the datatype of a specific column inside the body of the for-loop.
6. If you want to be sure you have correctly cleaned the dataset you can download a cleaned csv file and use that for the next part.
Download the cleaned .csv file [here](https://raw.githubusercontent.com/esciencecenter-digital-skills/2023-01-25-ds-python-rivm/main/data/Health__lifestyle__health_care_use_and_supply__causes_of_death__from_1900_21122022_143458_cleaned.csv).
You can right-click and press 'save as' to download it.

### 0.3. Dealing with topics and selecting the data of interest
The dataset is quite large, or at least there are a lot of different topics in there. 
(NB: the topics are the index, an example is 'Use of health care services|Contacts with health professionals|Dentist'): 
The topics are organized in a nested way, separated with '|'. 
For example: 'Use of health care services|Contacts with health professionals|Dentist' consists of 3 levels: 
'Use of health care services' (level 1), 'Contacts with health professionals' (level 2), and  'Dentist' (level 3). 
We will write some functions to create a better overview of the dataset and get quicker access to the different topics of our interest.
1. First figure out how to get the level 1 topic from a full topic description. Create a new string variable called topic: `topic = 'level 1| level 2 | level 3'`. Use the [`str.split`](https://www.w3schools.com/python/ref_string_split.asp) function and list indexing to get just the level 1 part of the string.
2. Create a function that returns a list with just the seven unique level 1 topics in the dataset. Hint 1: use your answer from the previous question. Hint 2: You can loop over the topics in the dataframe by doing `for topic in df.index:`.
3. Look at the code below. What does it do? Try it out! For example with `subset_data_starting_with(df, 'Use of health care services')`. Copy these functions to your notebook, it will be very handy for the next questions!

```python
def subset_data_starting_with(df, pattern):
    topics = df.index
    mask = topics.str.startswith(pattern)
    subset = df.iloc[mask].copy()
    return subset

def rename_to_last_level(df):
    mapper = dict()
    for topic in df.index:
        mapper[topic] = topic.split('|')[-1]
    df = df.rename(index=mapper)
    return df
```

## 1. Plotting contacts with health professionals
We will look at the 'Use of health care services|Contacts with health professionals' data.
We want to get a visual overview of how many people have contact with health professionals. 
But first, it's good to note that this is an aggregated dataset. 
Each value in the table actually comes from aggregating data of a lot of individuals. 
This is different from the dataset used in the course where every row corresponded with a single captured animal, and we had to aggregate it to plot. 

To help ourselves in plotting the data we will convert the data to the so-called 'long format' (you can read more about this [here](https://datacarpentry.org/python-socialsci/12-long-and-wide/index.html)). If you don't fully grasp it yet that's not a problem, just see it as a transformation of the data into a format that is handy for plotting. Here is the code for transforming our dataset to long format:

```python
def to_long_format(df):
    """
    Transforms the CBS health, lifestyle and causes of death dataset into 
    'long' format. In addition, drops the 'unit' column, and changes 'year'
    dtype to int.
    """
    df = df.drop(columns='unit')
    df['Topic'] = df.index # pd.melt cannot use the index so we have to create a column for it
    long_df = pd.melt(df, id_vars='Topic', var_name='year') 
    long_df['year'] = long_df['year'].astype(int)
    return long_df
```
1. Inspect the `to_long_format()` function. Compare the dataframes before and after passing it to the function. Can you make sense of what's happening and why?
2. Now try to answer 1a. Hint: Use the functions we defined previously to select the data, and transform it to long format. 
3. Now try to answer 1b. Hint: plotnine by default wants to plot the count of the values you pass it.
   Since our data is already aggregated we want to plot the actual values. You can do that by passing `stat='identity'` to the `geom_bar` function.

## 2. Health costs
One would expect that the percentage of people in good health would increase when the costs of our health system go up, is that true?
1. Take a look at the values for 'Care supply|Expenditures on care|Costs as a percentage of the GDP' and 'Health status|Persons in (very) good health'. What do you notice? 
   Hint: You can still use `subset_data_starting_with()` and use `pandas.concat()` to concatenate dataframes.
2. Now try to answer 2a
3. Now try to answer 2b. Hint 1: to calculate the indexed costs in 2000:
```python
costs_1990 = 10.9
costs_2000 = 10.0
indexed_costs_2000 = costs_2000 / 10.9 * 100
```
Hint 2: It is best to do the indexing operation before transforming the data to long format.
