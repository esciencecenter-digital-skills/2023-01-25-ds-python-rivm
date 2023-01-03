---
layout: page
title: "Post-workshop exercise"
---
## Introduction
We hope that after completing this exercise you have an idea of what it takes to analyse and visualize real-world data in python and that you can apply the learned skills to your own projects. 
For this exercise we use the 'health, lifestyle, health care use and supply, causes of death; from 1900' dataset from CBS opendata. 
This is quite a challenging dataset to work with. 
That is on purpose, we want this exercise to resemble your daily work as much as possible.

You can get a visual overview of the data [here]( https://opendata.cbs.nl/statline/#/CBS/en/dataset/37852eng/table?ts=1671446345991). 
For this exercise please use [this csv file](https://raw.githubusercontent.com/esciencecenter-digital-skills/2023-01-25-ds-python-rivm/data/Health__lifestyle__health_care_use_and_supply__causes_of_death__from_1900_21122022_143458.csv)
, right-click and click 'save as' to download it to your computer. 
We slightly adapted the format of the data so that it is easier to read into pandas. 

We want you to learn as much as possible from this exercise. 
If you are stuck for longer than 10 minutes, just have a look at [the solution notebook](https://github.com/esciencecenter-digital-skills/2023-01-25-ds-python-rivm/blob/main/files/solutions-post-workshop-exercise.ipynb). 
But do not keep the solutions next to you when going through the exercise. 
You can also ask Jurriaan (jurriaan.biesheuvel@rivm.nl), Xiaoheng (xiaoheng.huang@rivm.nl), or Markus (markus.viljanen@rivm.nl) for help. 

We expect you to take about 1 day to finish the exercise. See how far you get.

Imagine you have the task to explore the dataset and present your findings to your colleagues in a jupyter notebook. 
So make the graphs as readable as possible, 
and put some clarifying documentation in markdown cells around your code, it is good to practice this.

## 1. Loading the data
1. Load the data in pandas. (Hint: check the separator that is used in the file, you can pass a different separator to `read_csv()` using the `sep` argument)
2. Take a look at the data. As you can see, the Topic is read as a column and not as index. You can fix this by passing `index_col='Topic'` to `read_csv()`.

## 2. Cleaning up the data
1. Take a look at the data. How are missing data represented?
2. Replace the value that is used for missing data with NaN. (hint: You can replace values using DataFrame.replace(). You can use numpy.nan to represent NaN values)
3. Rename the 'Unnamed: 1' column to 'unit'
4. What is the datatype of the numerical values?
5. Convert all data in the numerical columns (all columns excluding 'unit') to the 'float' datatype. Use a for-loop to loop over all the numerical columns. Change for a specific column inside the body of the for-loop.

## 3. Getting an overview of the data
The dataset is quite large, or at least there are a lot of different topics in there. The topics are organized in a nested way, for example: 'Use of health care services|Contacts with health professionals|Dentist' consists of 3 levels: 'Use of health care services' (level 1) 'Contacts with health professionals' (level 2) 'Dentist' (level 3). We will write some functions to create a better overview of the dataset and get quicker access to the different topics of our interest.
1. First figure out how to get the level 1 topic from a full topic description. Create a new variable called topic: `topic = 'level 1| level 2 | level 3'`. Use the [`str.split`](https://www.w3schools.com/python/ref_string_split.asp) function and list indexing to get just the level 1 part of the string.
2. Create a function that returns a list with just the seven level 1 topics in the dataset. Hint 1: use your answer from the previous question. Hint 2: You can loop over the topics in the dataframe by doing `for topic in df.index:`.
3. Look at the code below. What does it do? Try it out! For example with `subset_data_starting_with(df, 'Use of health care services'`. Copy these functions to your notebook, it will be very handy for the next questions!

```python
def subset_data_starting_with(df, pattern):
    mask = df.index.str.startswith(pattern)
    subset = df.iloc[mask].copy()
    return subset

def rename_to_last_level(df):
    mapper = dict()
    for topic in df.index:
        mapper[topic] = topic.split('|')[-1]
    df = df.rename(index=mapper)
    return df
```

## 4. Plotting contacts with health professionals
We will look at the 'Use of health care services|Contacts with health professionals' data. We want to get a visual overview of how many people have contact with health professionals. But first, it's good to note that this is an aggregated dataset. Each value in the table actually comes from aggregating data of a lot of individuals. This is different from the dataset used in the course where every row corresponded with a single captured animal, and we had to aggregate it to plot. 

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
2. Create a linegraph that shows the percentage of people having contact with a health professional for each category over time. The different categories (General practitioner (GP), Medical specialist, Dentist, Physiotherapist or exercise therapist, and Alternative healer) should show as different colored lines in the linegraph. Hint: Use the functions we defined previously to select the data, and transform it to long format. 
3. Create a bargraph that shows the percentage of people having contact with a health professional for each category (General practitioner (GP), Medical specialist, Dentist, Physiotherapist or exercise therapist, and Alternative healer) in **2021**. Hint: plotnine by default wants to plot the count of the values you pass it. Since our data is already aggregated we want to plot the actual values. You can do that by passing `stat='identity'` to the `geom_bar` function.

## 5. AIDS/HIV
We will now look at how the number of people infected with HIV and the number of people that developed AIDS developed over the years.
1. Make a lineplot with the years on the x-axis and the number of notifications on the y-axis. 
One line should represent the number of people that developed AIDS and the other line the number of HIV-infected people.

## 6. Health costs
One would expect that the percentage of people in good health would increase when the costs of our health system go up, is that true?
1. Take a look at the values for 'Care supply|Expenditures on care|Costs as a percentage of the GDP' and 'Health status|Persons in (very) good health'. What do you notice? Hint: You can still use `subset_data_starting_with()` and use `pandas.concat()` to concatenate dataframes.
2. Create a lineplot with the years on the x-axis and percentage y-axis. One line should represent the health costs as a percentage of the GDP, while the other line should show the percentage of people in (very) good health. Is this a good way of visualizing the data?
3. One way to visualize this data in a better way is to index it based on 1990. We make the values in 1990 100, and then for later years take the value relative to the value in 1990. So to calculate the indexed costs in 2000:
```python
costs_1990 = 10.9
costs_2000 = 10.0
indexed_costs_2000 = costs_2000 / 10.9 * 100
```
Calculate the indexed data and plot it in a lineplot. Hint: It is best to do the indexing operation before transforming the data to long format.

## 7. Bonus question: another dataset
Have a look at the [other CBS opendata datasets](https://opendata.cbs.nl/statline/#/CBS/en/navigatieScherm/thema). Pick a dataset that you like. Come up with interesting questions about the data and try to answer them using data analysis.
