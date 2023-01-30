![](https://i.imgur.com/iywjz8s.png)


# Collaborative Document 2023-01-25 Python RIVM

Welcome to The Workshop Collaborative Document.

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents.

----------------------------------------------------------------------------

This is the document for today: [https://tinyurl.com/2023-01-25-rivm](https://tinyurl.com/2023-01-25-rivm) 

## 👮Code of Conduct

Participants are expected to follow these guidelines:
* Use welcoming and inclusive language.
* Be respectful of different viewpoints and experiences.
* Gracefully accept constructive criticism.
* Focus on what is best for the community.
* Show courtesy and respect towards other community members.
 
## ⚖️ License

All content is publicly available under the Creative Commons Attribution License: [creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/).

## 🙋Getting help

To ask a question, just raise your hand.

If you need help from a helper, place an orange post-it note on your laptop lid. A helper will come to assist you as soon as possible.

To signal that you are done with an exercise, place the blue post-it on your laptop lid. 

## 🖥 Workshop website

[Link to workshop website](https://esciencecenter-digital-skills.github.io/2023-01-25-ds-python-rivm/)

[Link to post-workshop exercise](https://esciencecenter-digital-skills.github.io/2023-01-25-ds-python-rivm/post-workshop-exercise.html)

## 👩‍🏫👩‍💻🎓 Instructors

Sven van der Burg, Jaro Camphuijsen

## 🧑‍🙋 Helpers

Jurriaan van Biesheuvel, Xiaoheng Huang, Markus Viljanen

## 👩‍💻👩‍💼👨‍🔬🧑‍🔬🧑‍🚀🧙‍♂️🔧 Roll Call
Name/ pronouns (optional) / job, role / social media (twitter, github, ...) / background or interests (optional) / city

## 🗓️ Agenda
| time  | what                                                  |
|-------|-------------------------------------------------------|
| 09:30 | Welcome and icebreaker                                |
| 09:45 | What is Python and why should I learn it?             |
| 10:00 | Introduction to Programming in Python                 |
| 10:30 | Break                                                 |
| 10:40 | Starting With Data                                    |
| 11:30 | Break                                                 |
| 11:40 | Indexing, Slicing and Subsetting DataFrames in Python |
| 12:30 | Lunch Break                                           |
| 13:30 | Data Types and Formats                                |
| 14:00 | Combining DataFrames with Pandas                      |
| 14:30 | Break                                                 |
| 14:40 | Data Workflows and Automation                         |
| 15:30 | Break                                                 |
| 15:40 | Making Plots With plotnine                            |
| 16:30 | Wrap-up & post-workshop exercise introduction                                              |
| 17:00 | END                                                   |

## 🏢 Location logistics
* Coffee --> Will be provided in the breaks, everyone except Jaro and Sven knows where the coffee machine is
* Toilets? --> just around the corner
* Wifi? --> everyone has access
* Emergency exit? --> out of the door, to the left

## 🎓 Certificate of attendance
If you attend the full workshop you can request a certificate of attendance by emailing to training@esciencecenter.nl .

## 🔧 Exercises

#### Challenge - DataFrames

Using our DataFrame `surveys_df`, try out the attributes & methods below to see
what they return.

1. `surveys_df.columns`
2. `surveys_df.shape` Take note of the output of `shape` - what format does it return the shape of the DataFrame in?

HINT: [More on tuples, here][python-datastructures].
3. `surveys_df.head()` Also, what does `surveys_df.head(15)` do?
4. `surveys_df.tail()` Also, what does `surveys_df.tail'* do


#### Challenge - Statistics

1. Create a list of unique site ID's ("plot_id") found in the surveys data. Call it
`site_names`. How many unique sites are there in the data? How many unique
species are in the data?

*
* R
2. (optional) What is the difference between `len(site_names)` and `surveys_df['plot_id'].nunique()`?




#### Challenge - Summary Data

1. How many recorded individuals are female `F` and how many male `M`?
https://stackoverflow.com/questions/22391433/count-the-frequency-that-a-value-occurs-in-a-dataframe-column


2. What happens when you group by two columns using the following syntax and then calculate mean values?
- `grouped_data2 = surveys_df.groupby(['plot_id', 'sex'])`
- `grouped_data2.mean()`


3. Summarize weight values for each site in your data. HINT: you can use the following syntax to only create summary statistics for one column in your data.
`by_site['weight'].describe()`
 

### Feedback 
#### What is something you liked about the morning?
* getting a rough idea about what python is and to what extent it is of added value compared to R
* good atmosphere in the course! 
* well paced introduction, nice exercises also the optional one. 
* nice introduction, enough help provided when needed
* enough attention on pace and time for questions.
*good speed second part of the morning
* speed 
* could understand it well, nice exercises
* + you guys are very nice
*nice introduction
* Really well-introduced with a om not only for content but only for expectations/experience etc. from audience
* Nice pace of the exercises
* pace of the explanation and exercises
* Good introduction to the basics
* Good build up of basics
#### What is something you would like to see improved in the afternoon?

* explanation of difference between console, terminal, notebook

* Some links to good resources or books or tutorials 

* Get an idea to what extent Python can replace R, is it accepted by medical journals? be applied 
* Already have the list of names here so you don't mess up the format by typing your name! ;) 
* second the above!



* *
* Move a bit up to some more challenging taks
* a cheat sheet for all the basics of python 
* softwarelenging taks
* Better explanation of attribute vs method vs function and pandas vs 'base' python


#### Challenge - Plots

1. Create a plot of average weight across all species per site.


2. Create a plot of total males versus total females for the entire dataset.




#### (Optional) Summary Plotting Challenge

Create a stacked bar plot, with weight on the Y axis, and the stacked variable being sex. The plot should show total weight by sex for each site. Some tips are below to help you solve this challenge:

* For more information on pandas plots, see [pandas' documentation page on visualization][pandas-plot].
* You can use the code that follows to create a stacked bar plot but the data to stack need to be in individual columns.  Here's a simple example with some data where 'a', 'b', and 'c' are the groups, and 'one' and 'two' are the subgroups.

```python
d = {'one' : pd.Series([1., 2., 3.], index=['a', 'b', 'c']), 'two' : pd.Series([1., 2., 3., 4.], index=['a', 'b', 'c', 'd'])}
pd.DataFrame(d)
```

shows the following data

```
one  two
a    1    1
b    2    2
c    3    3
d  NaN    4
```

We can plot the above with

```
# Plot stacked data so columns 'one' and 'two' are stacked
my_df = pd.DataFrame(d)
my_df.plot(kind='bar', stacked=True, title="The title of my graph")
```

![Stacked Bar Plot](https://datacarpentry.org/python-ecology-lesson/fig/stackedBar1.png)

* You can use the `.unstack()` method to transform grouped data into columns for each plotting.  Try running `.unstack()` on some DataFrames above and see what it yields.

Start by transforming the grouped data (by site and sex) into an unstacked layout, then create a stacked plot.

#### Challenge - Range

1. What happens when you execute:

- `surveys_df[0:1]`
- `surveys_df[:4]`
- `surveys_df[:-1]`

2. What happens when you call:

- `surveys_df.iloc[0:4, 1:4]`
- `surveys_df.loc[0:4, 1:4]`

3. How are the two commands different?


#### Challenge - Queries

1. Select a subset of rows in the `surveys_df` DataFrame that contain data from the year 1999 and that contain weight values less than or equal to 8. How many rows did you end up with? What did your neighbor get?

2. You can use the `isin` command in Python to query a DataFrame based upon a list of values as follows:

~~~
surveys_df[surveys_df['species_id'].isin([listGoesHere])]
~~~

Use the `isin` function to find all plots that contain particular species in the "surveys" DataFrame. How many records contain these values?

3. Experiment with other queries. Create a query that finds all rows with a weight value > or equal to 0.

4. The `~` symbol in Python can be used to return the OPPOSITE of the selection that you specify in Python. It is equivalent to **is not in**. Write a query that selects all rows with sex NOT equal to 'M' or 'F' in the "surveys" data.


## Collaborative notes
### What is Python?
* Python is a general purpose programming language that supports rapid development of data analytics applications. 
* The word “Python” is used to refer to both, the programming language and the tool that executes the scripts written in Python language.

### So, why should you learn Python?
* Better and more packages and documentation in Python
* Existing programs in python that we are forced to use/adapt
* Fairly easy to learn compared to other programming languages
* Some people prefer Python (this is the case for every language)
* Python is very versatile, can be used for web applications as well as hard core machine learning
* Python's community is big and active, you can (almost) always find a solution to your problem (just search for it: Ecosia? ;-) )
* Open source, everyone can use it (you don't have to buy a license)

### Sven's opinion on R and python
* Everything we will learn today, you can do in R
* But R is domain specific, Python is more versatile, not just statistics and data
* if you need to keep doing what you're already doing, stay with what you know, but if you are interested in contributing to bigger and different projects, try python

### Get in the cloud environment
* go to: https://rivm-ood-l01t.rivm.ssc-campus.nl/
* To open a new notebook: click on the 'left' button: python3 ipykernel

### Python from the terminal
You can open python in the terminal (also called 'command prompt') by typing `python`
You can run python code interactively from here.

You can type in python code in a 'script', a text file with the .py extension.

### Jupyter notebooks
A notebook is something in between 'scripting' and interactive terminal.
You can change the type of the cell -> markdown/code

Shortcut for executing a cell: shift + enter

Shortcut for changing a cell to markdown: change view from 'inside' a cell to 'on top of' a cell by pressing 'Esc'. Then type 'M' to change it to markdown.

### Creating variables
```python
text = "Data Carpentry"
number = 4  # number is the variable name, # 4 is the value it stores
pi_value = 3.1415
```

### Variable types
Checking the type of a variable:
```python=
type(text)
```
```python=
type(number)
```
```python=
type(pi_value)
```

int -> integer: whole numbers (no decimals)
float -> floating point number: Numbers with decimal precision

### Printing
```python
print(text)
```
Scripts will not output the actual value of a variable (this is inert to ipython notebooks)

### Built-in Python functions
`type()` and `print()` are built-in Python functions

### Operators
```python=
complicated = 3 + 6 - 6 / 3 * 5
complicated
```

Modulo
```python=
13 % 5
```

Logic operators
```python=
3 > 4  # false
5 == 5 # true
number > pi_value # true
(3 > 2) and (2 > 4) # false
```

### 2 or 1 equal sign?
2 equal signs (`==`): compare values
1 equal sign (`=`): assign value to variable

### Lists
```python=
numbers = [1, 2, 3] # Create a list with 3 values
numbers[0] # Select the first element in the list
```
Python is 0-indexed, this means we start counting at 0 (compare this to other lanuages like R that are 1-indexed)

```python=
numbers[3] # Throws an IndexError
```

Append a value to a list:
```python=
numbers.append(4)  # adds 4 to the end of the list
```
#### methods
A 'method' is a function that is 'attached' to an object. For example `.append()` is a method of `numbers`. 

### Getting help in Python
```python=
help(list) # Get help on the class 'list'
help(numbers) # Get help on the 'number' variable
```

### Dictionaries
Define a dictionary with curly braces {}
```python
translation = {'one': 'first', 'two': 'second'}
translation['one'] # access the value that is associated to the 'one' key
```

## Starting with data 
New notebook "2.starting-with-data.ipynb"

Download data (full zip) from on your computer https://figshare.com/articles/dataset/Portal_Project_Teaching_Database/1314459

Unzip the zip file and upload the files to the cloud environment. Create a new folder in the could environment to hold the data.

In Python you can import packages using the `import` statement:

```python=
import pandas as pd
```

We use the shorthand pd, so that we don't have to type pandas every time we want to use a function from the package. We will assign it to a new variable.

```python=
surveys_df = pd.read_csv("data/surveys.csv") #df = dataframe
```

We can check the types of the columns in our dataframe

```python=
surveys_df.dtypes
```

There are more attributes and objects of the dataframe object

```python=
surveys_df.columns #gives the column names
surveys_df.head(3) #gives first three rows of df
```

### Looking at values 
We can select a specific column using the column name

```python=
species = surveys_df['species_id']
```

And we can look at unique values in a column using another pandas function

```python=
pd.unique(species)
```

> #### Challenge - Statistics
> 
> 1. Create a list of unique site ID's ("plot_id") found in the surveys data. Call it
> `site_names`. How many unique sites are there in the data? How many unique
> species are in the data?
> 
> ```python=
> site_names = pd.unique(surveys_df['plot_id']) #a list of site names 
> len(site_names) # give the length of the list 'site_names'
> ```

Another helpful method can be used to describe the statistics of a dataframe:

```python=
surveys_df['weight'].describe()
```
Or per statistic type:
```python=
surveys_df['weight'].min()
surveys_df['weight'].max()
surveys_df['weight'].mean()
surveys_df['weight'].std()
surveys_df['weight'].count()
```


### Groups in pandas
Often it is usefule to group the data by certain attributes:
```python= 
# Group data by sex
grouped_data = surveys_df.groupby('sex')
```


### Quick and dirty plotting
```python=
# tell jupyter to show figures inline
%matplotlib inline

# create a quick bar chart
species_counts = surveys_df.groupby('species_id')['record_id'].count()
# or
species_counts = surveys_df['species_id'].value_counts()

species_counts.plot(kind='bar')
```

#### Challenge - Plots

1. Create a plot of average weight across all species per site.

```python=
grouped_data = surveys_df.groupedby('plot_id')
grouped_data_mean_weight = grouped_data["weight"].mean
grouped_data_mean_weight.plot(bar)
```

2. Create a plot of total males versus total females for the entire dataset.

```python=
sex_counts = surveys_df['sex'].value_counts()
sex_counts.plot(kind='bar')
```

### Slicing and combining dataframes
There is no shared memory between notebooks, so we need to import libraries and read in data again.
```python=
import pandas as pd
# This assumes your notebook lives in the root folder `/`
surveys_df = pd.read_csv('data/surveys.csv') 
```

`[*]` in front of a cell means it's being executed

Two ways of accessing a column from the dataframe:
```python=
surveys_species = surveys_df['species_id']
surveys_species = surveys_df.species_id
```

Accessing multiple columns:
```python=
surveys_subset = surveys_df[['species_id', 'plot_id']]
```

Selecting multiple rows:
```python=
surveys_df[0:4] # Select first 4 rows (row 0 until 3 (upper limit is not included in range))
surveys_df[:6] # From first row up to row 5 (the 6th row)
surveys_df[-5:] # Last 5 rows of the dataset
surveys_df[-5:-1] # From -5 th row up to but not including the last row (-1th row)
```

#### Copies and references of variables
In Python there is an important difference between referring and copying a variable!
```python=
# This creates a reference to the same dataframe
# changes in `surveys_df2` will actually change `surveys_df`
surveys_df2 = surveys_df 
# This copies the dataframe to a new variable
# changes in `surveys_df2` will **not** change `surveys_df`
surveys_df2 = surveys_df.copy() 
```

#### indexing with iloc
```python
surveys_df.iloc[0:3, 1:4] # select first 3 rows and 2nd to 4th column
```

#### indexing with loc
```python=
surveys_df.loc[0:5, ['species_id', 'species_id']]
```

#### Exercise: range
```python=
surveys_df.iloc[0:4, 1:4]# select first 4 rows and 2nd to 4th column
surveys_df.loc[0:4, 1:4] # Throws error, you can not index with integers, it wants column names
```

#### Subsetting data using criteria
```python=
surveys_df[surveys_df.year == 2002] # Select subset of data where year is 2002 
surveys_df[surveys_df.species_id == "DM"] # Select subset of data where species is DM
surveys_df[surveys_df.species_id != "DM"] # Select subset of data where species is NOT DM
# Select subset of data where species is DM AND year is 2002
surveys_df[(surveys_df.species_id == 'DM') & (surveys_df.year == 2002)]
```

#### Concatenating
```python=
surveys_head = surveys_df.head(5)
surveys_tail = surveys_df.tail(5)
vertical_stack = pd.concat([surveys_head, surveys_tail], axis=0)
```
0-axis is vertical, 1-axis is horizontal

Also take a look at the documentation of `pd.Dataframe.merge()` for more complex combining of dataframes.

### Data types and formats & missing values

```python=
#check the type of a column
surveys_df["record_id"].dtype
#change the type of a whole column
surveys_df['record_id'] = surveys_df['record_id'].astype('float64')
```

```python=
#make a list of boolean values (True or False) that tells us whether a weight value is missing
pd.isnull(surveys_df.weight)
# select all the rows with a missing weight
rows_with_nan_values = surveys_df[pd.isnull(surveys_df.weight)]
```

To deal with missing values there are several useful functions:

```python=
rows_with_nan_values = surveys_df[pd.isnull(surveys_df)]

surveys_df['weight'] = surveys_df['weight'].fillna(surveys_df['weight'].mean())
```

### Loops and functions
* Can I automate operations in Python?
* What are functions and why should I use them?

#### For loops
```python=
animals = ['lion', 'tiger', 'crocodile']

print(animals)

for creature in animals:
    print("Sven is cool")
    print(creature)
print('Sven is not cool')
```

## Use for loops to automate reading in subsets of data

```python=
import pandas as pd
surveys_df = pd.read_csv('data/surveys.csv')
#make a new subset of the data
surveys_2002 = surveys_df[surveys_df.year == 2002]

```

We will first write our data to a new csv file and use the `os` library for that

```python=
import os
os.mkdir('data/yearly_files')

surveys_2002.to_csv('data/yearly_files/surveys2002.csv')
```
If you want to do this for every year in the dataset, that will take a lot of lines of code, it is better to do it automatically in a for-loop:

```python=
all_the_years = surveys_df['year'].unique()

for year in all_the_years:
    filename = f'data/yearly_files/surveys{year}.csv' #this is a so called "f-string"
    surveys_for_one_year = surveys_df[surveys_df.year == 2002]
    surveys_for_one_year.to_csv('data/yearly_files/surveys2002.csv')

```

### Functions
If you find yourself repeating a particular piece of code multiple times, you probably want to make a function out of it. Then you can just call that function instead of repeating the code.

```python=
def subset_by_year(year, df):
    """
    Selects the data given 'year' input argument
    Writes the data to the yearly files folder for that specific year.
    """
    filename = f'data/yearly_files/surveys{year}.csv'
    surveys_for_one_year = df[surveys_df.year == 2002]
    surveys_for_one_year.to_csv('data/yearly_files/surveys2002.csv') #writes the survey to a csv 
    return surveys_for_one_year #this makes the subset available to you after you execute the function
```


Now we can use that function in the for-loop:

```python=
for year in all_the_years:
    subset_by_year(year, surveys_df)
```

```python=
%matplotlib inline

import plotnine as p9

surveys_complete = surveys_df.read_csv('data/surveys.csv')

(p9.ggplot(data=surveys_complete,
           mapping = p9.aes(x='weight', y='hindfoot_length'))
 + geom_point()
)
```

Same plot but more readable:
```python=
surveys_plot = p9.ggplot(data=surveys_complete,
                         mapping = p9.aes(x='weight', y='hindfoot_length'))
surveys_plot + geom_point()
```

Plotting with colours :rainbow:
```python=
surveys_plot = p9.ggplot(data=surveys_complete,
                         mapping = p9.aes(x='weight', 
                                          y='hindfoot_length',
                                          color='species_id'))
surveys_plot + geom_point()
```

## 📚 Resources
* [Link to post-workshop exercise](https://esciencecenter-digital-skills.github.io/2023-01-25-ds-python-rivm/post-workshop-exercise.html)
* [eScience center webiste](esciencecenter.nl)
* [Digital skills program](https://www.esciencecenter.nl/digital-skills/)
* Research software engineers [nl-rse.org](nl-rse.org)
* [Portal teaching database](https://figshare.com/articles/dataset/Portal_Project_Teaching_Database/1314459)
* [Python cheat sheet](https://perso.limsi.fr/pointal/_media/python:cours:mementopython3-english.pdf)
* [Pandas cheat sheet](http://datacamp-community-prod.s3.amazonaws.com/f04456d7-8e61-482f-9cc9-da6f7f25fc9b)

How to proceed?:
* Read about the [Zen of Python](https://peps.python.org/pep-0020/)
* Checkout the NLeSC [guide on Python](https://guide.esciencecenter.nl/#/best_practices/language_guides/python)
* Read the book ['effective Python: 59 specific ways to write better Python'](https://effectivepython.com/)
* Setting up an environment on your own machine: [setup instructions](https://datacarpentry.org/python-ecology-lesson/setup.html)
* Read about virtual environments: [virtual environments](https://carpentries-incubator.github.io/python-intermediate-development/12-virtual-environments/index.html)

* Read the book on [grammar of graphics](https://link.springer.com/book/10.1007/0-387-28695-0)

### Post-workshop survey
https://www.surveymonkey.com/r/5PBTZYB
