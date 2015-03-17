# Working With Dataframes in Python


### Learning Objectives
* Explain what a library is, and what libraries are used for.
* Load a Python/pandas library and use the things it contains.
* Read tabular data from a file into a program.
* Assign values to variables.
* Learn about data types
* Select individual values and subsections from data.
* Perform operations on arrays of data.
* Display simple graphs.

##About Libraries
A library in Python, contains a set of tools (called functions) that perform tasks that we might want to complete on our data. Importing a library is like getting a piece of lab equipment out of a storage locker and setting it up on the bench for use in analysis. Once it's setup, the library can be used or called to perform many tasks for us.

##Pandas in Python
One of the best options for working with tabular data in python, is to use the [Python Data Analysis Library](http://pandas.pydata.org/) (a.k.a. pandas) library. The Pandas library provides data structures, produces high quality plots with [matplotlib](http://matplotlib.org/), and integrates nicely with other libraries that expect [NumPy](http://www.numpy.org/) arrays.

Python doesn't load all of the libraries available to it by default. We have to add an import statement to our code prior to called the functions within the library first. To do this, we use the syntax `import` libraryName `as` nickNameHere you want.  


```python
import pandas as pd
```

In the example above, we have imported pandas as pd. `pd` a nice shortcut so we don't have to type out `pandas` each time we call a pandas function. Anytime we want to call a pandas function we can type `pd.FunctionName`


##Lesson Overview

We are studying the species and weight of animals caught in plots in our study area.
The data sets are stored in .csv (comma separated value) format. Within the `.csv` files, each row holds information for a single animal,
and the columns represent: record_id, month, day, year, plot, species, sex, wgt. 

The first few rows of our first file look like this:

"63","8","19","1977","3","DM","M","40"

"64","8","19","1977","7","DM","M","48"

"65","8","19","1977","4","DM","F","29"

"66","8","19","1977","4","DM","F","46"

"67","8","19","1977","7","DM","M","36"

### We want to:

1. Load that data into memory in Python,
2. Calculate the average weight of the animals for all species.
3. Plot the average weights by species ((IS THIS RIGHT??)

We can automate this process above, using Python programming! It's efficient to spend this time building the code to perform these tasks because once it's built, we can use it over and over on different datasets that use a similar format! This makes our methods easily reproducible.  


# DO WE NEED THIS IF THEY HAVE PANDAS INSTALLED? Should we check to see if pandas is installed.
#also if they are using anaconda it might need to be conda install pandas. i think this belongs in the workshop overview.

### Installing pandas

If you use pip installing pandas should be easy:

```
[user@host:python]$sudo pip install pandas
```

For more complex scenarios, please see the [installation instructions](http://pandas.pydata.org/pandas-docs/stable/install.html).

To start working with pandas user should open ipython shell in folder with python lessons

```
[user@host:python]$ipython
```



# Reading Data Using Pandas CSV
We will begin by locating and reading our data. The data are in CSV format so we can use pandas' `read_csv` function to pull it directly into a [DataFrame](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe). A dataframe is a 2-dimensional data structure that can store data of different types in columns. It is similar to spreadsheets or SQL tables or the `data.frame` in R. It can store a mix of data types, including characters, integers, floating point values, factors and more. 

Let's begin by loading the `surveys.csv` file into python. 

#DIRECTORIES NEED TO BE SET FOR THIS TO WORK PROPERLY -- I DID THIS IN SOFTWARE CARPENTRY _ SHOULD WE DO THIS HERE??

First, let's make sure the python Pandas library is loaded. It's common practice to load the pandas library using the name `pd`. If we do that, then each time we use a pandas function, like read_csv, we will only have to type pd instead of the full name, pandas.

```python
import pandas as pd
```

Let's also import the OS library. This library will allow us to make sure we are in the correct working directory.

	import OS
	os.getcwd()
	

```python
#note the pd.read_csv is used because we imported pandas as pd
pd.read_csv("data/biology/surveys.csv")
```

The above command yields the **output** below:

```
       record_id  month  day  year  plot species  sex  wgt
0              1      7   16  1977     2     NaN    M  NaN
1              2      7   16  1977     3     NaN    M  NaN
2              3      7   16  1977     2      DM    F  NaN
3              4      7   16  1977     7      DM    M  NaN
4              5      7   16  1977     3      DM    M  NaN
5              6      7   16  1977     1      PF    M  NaN
6              7      7   16  1977     2      PE    F  NaN
7              8      7   16  1977     1      DM    M  NaN
8              9      7   16  1977     1      DM    F  NaN
9             10      7   16  1977     6      PF    F  NaN
10            11      7   16  1977     5      DS    F  NaN
11            12      7   16  1977     7      DM    M  NaN
12            13      7   16  1977     3      DM    M  NaN
13            14      7   16  1977     8      DM  NaN  NaN
...
[35549 rows x 8 columns]
```


Let's call the imported data `dat`: 

```python
dat = pd.read_csv("data/surveys.csv")
```

Notice when you assign the imported dataframe to a variable, python does not produce any output on the screen. We can print the `dat` object by typing in its name into the python command prompt.

```python
dat
```

which gives **output**


```
       record_id  month  day  year  plot species  sex  wgt
0              1      7   16  1977     2     NaN    M  NaN
1              2      7   16  1977     3     NaN    M  NaN
2              3      7   16  1977     2      DM    F  NaN
3              4      7   16  1977     7      DM    M  NaN
4              5      7   16  1977     3      DM    M  NaN
5              6      7   16  1977     1      PF    M  NaN
6              7      7   16  1977     2      PE    F  NaN
7              8      7   16  1977     1      DM    M  NaN
8              9      7   16  1977     1      DM    F  NaN
9             10      7   16  1977     6      PF    F  NaN
10            11      7   16  1977     5      DS    F  NaN
11            12      7   16  1977     7      DM    M  NaN
12            13      7   16  1977     3      DM    M  NaN
13            14      7   16  1977     8      DM  NaN  NaN
...
[35549 rows x 8 columns]
```

We can figure out the type of object that dat is by typing:

	type(dat)

OUTPUT:

	pandas.core.frame.DataFrame


## Manipulating Our Species Survey Data

Now we can start manipulating our data! First, let's check data type of object that `dat` is using the `type` command. The `type` function and `__class__` attribute tell us that `dat` is `<class 'pandas.core.frame.DataFrame'>` in Python. 

```python
type(dat)
#this does the same thing as the above!
dat.__class__
```
We can also use the `dat.dtypes` command to view the data type within each column in our dataframe. 

	dat.dtypes

which gives **output**:

```
record_id      int64
month          int64
day            int64
year           int64
plot           int64
species       object
sex           object
wgt          float64
dtype: object
```
#WE SHOULD SOMEHOW OVERVIEW WHAT ALL OF THESE THINGS ARE. 

### Useful Ways to View DataFrame objects in Python

There are multiple methods that can be used to summarize and access the data stored in dataframes. Let's try out a few. Note that we call the method by using the object name `dat.method`. So `dat.columns` provides an index of all of the column names in our dataframe. Try out some of the other methods below.  

#### Useful methods
* `dat.columns` - names of columns
* `dat.head()` - displays 5 first rows
* `dat.tail()` - displays 5 last rows
* `dat.shape` - gives shape of  data in tuple (rows, columns)


# Indexing in Python
If we want to get a single value from the **DataFrame** object we must provide an index to it in square brackets and use iloc function.

```python
dat.iloc[2,6]
```

which gives **output**
```
'F'
```

You have to remember that in Python indexing run from 0. Index like (2, 6) selects a single element of an array. We can also select whole sections as well. For example, we can select month, day and year (columns form second to fourth) of values for the first three rows(rows) like this:

```python
dat.iloc[0:3, 1:4]
```
which gives **output**
```
   month  day  year
0          1      7   16  1977
1          2      7   16  1977
2          3      7   16  1977
```

Slice 1:3 means "Start at index 1 and go to index 3, but not include values at index 4".

We can also use built-in function range to take regurally spaced rows and columns.
In this example we get rows 1, 3 and column 1, 3 and 5

```python
dat.iloc[range(1, 7, 2), range(1, 7, 2)]
```

which gives **output**
```
   month  year species
1      8  1977      DM
3      8  1977      DM
```

__EXERCISES__


## Calculating statistics


We've gotten our data in Python, so that we can do some analytics with it.
First, let's get a sense of our data in file surveys.csv
We might for instance want to know how many animals we trapped in each plot, or how many of each species were caught.
We can look at one column in diifferent ways. We can refere tha column by its number:

```python
dat.iloc[:,7]
```

or by name:

```python
dat.month
dat['month']
```

If you forget the column names, you can type

```python
dat.columns.values
```

which gives **output**:

```
array(['record_id', 'month', 'day', 'year', 'plot', 'species', 'sex', 'wgt'], dtype=object)
```


So, let's get a list of all the species.
The pandas.unique function tells us all the unique names in that column.

```python
pandas.unique(dat.species)
```

Now let's see how many of each species we have:

```python
dat.record_id.groupby(dat.species).nunique()
```

We could even assign it to a variable and make it a DataFrame to make it easier to look at:

```python
species_table = dat.record_id.groupby(dat.species).nunique()
```

Maybe we also want to see how many animals were captured in each plot

```python
dat['plot'].groupby(dat.species).nunique()
```

Now we want to do some actual calculations with the data though.
Let's calculate the average weight of all the animals. Python pandas has a finction describe, that give a lot of statistical informations, like mean, median, max, min, std and count. Describe can be olny used on numeric column.

```python
dat['wgt'].describe()
```
gives **output**

```python
count    32283.000000
mean        42.672428
std         36.631259
min          4.000000
25%         20.000000
50%         37.000000
75%         48.000000
max        280.000000
dtype: float64
```

Also we can use just one of this functions:

```python
dat['wgt'].min()
dat[wgt'].max()
dat['wgt'].mean()
dat['wgt'].std()
dat['wgt'].count()
```


Because data is in a vector, when we want to know how much of something we have we ask how long it is with the len() function.

```python
len(dat['wgt'])
```

## Statistics on subsets of data

When analyzing data, though, we often want to look at partial statistics, such as the maximum value per species or the average value per plot.
One way to do this is to select the data we want to create a new temporary array.

```python
dat[dat.species == 'DO']
```

We could see in our table from before that 'DO' had 3027 species.
Let's check to see if that's what we have by checking the number of rows:

```python
dat.record_id.groupby(dat['species']).nunique()['DO']
```

## FUNCTIONS
