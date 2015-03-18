# THIS ACTIVITY NEEDS TO BE REASSESSED -- ALSO NEED TO COMPARE LESSON 05 TO LESSON 01 AND 02 FOR REDUNDANCY!

# Extracting and Viewing Slices of our DataFrame - Indexing & Slicing in Python
We often want to work with subsets of our  **DataFrame** object. There are different ways to accomplish this, using labels (column headings, numeric ranges, or specific x,y index locations). 


##Selecting Data Using Labels (Column Headings)

We use square brackets `[]` to select a subset of an Python object. For example, we can select a column within the surveys dataframe by name:

	dat['species']
	#the syntax below gives you the same output
	dat.species

We can also set a variable to be a subset of a dataset we are working with (for example the column containing species data). 

	surveys_species=dat['species']

We can pass a list of columns to select columns in that order. This is useful for applying a function (like transform) to a subset of your columns.  NOTE: If a column is not contained in the dataframe, an exception (error) will be raised. 
	
	#select the species and plot columns from the DataFrame
	surveys[['species', 'plot']]

We can also access columns within DataFrames as an attribute:

	dat.wgt

##Extracting Range based Subsets: Slicing 

Slicing using the [] operator selects a set of rows or columns from a dataframe. When slicing in pandas the start bound and the stop bound are included. data[start:stop]

	#select the first, second and third rows from the surveys variable
	dat[0:3]
	#select the first 5 rows (not including row with the index value of 6)
	dat[:5]
	#select the second to last row
	dat[-1:]


We can also create new objects by slicing out parts of a DataFrame. 

	#copy the surveys dataframe
	surveys_copy=dat
	
	#set the first three rows of data in the dataframe to 0
	surveys_copy[0:3]=0

##Data Slicing in Python
We can use the same syntax to slice out a subset of data from our DataFrame. For example, we can select month, day and year (columns 2,3 and 4 if we start counting at 1), like this:

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

Notice anything odd about the output above? We asked for a slice that goes from 0:3. Wouldn't that suggest that python would select 4 rows in total? Another unique aspect of python is that when you slice a subset of data from `0:3`, you are actually telling python to start at index 0 and select rows 0,1,2 **up to but not including 3**. This might be confusing at first, but you'll get used to it with time. 


## Index based subsets

We can also select specific ranges of our data in both the row and column direction using the `loc` and `iloc` arguments. The `loc' argument allows you to select data using labels AND numeric integer locations. `iloc` only allows you to select ranges using labels, `loc` only accepts integer index values.

NOTE: Index values and labels must be in the DataFrame or you will get a KeyError. Remember that the start bound and the stop bound are included. When using `loc` Integers can be used, but they refer to the index label and not the position.

	#select all columns for rows of index values 0 and 10
	dat.loc[[0,10],:]
	#what does this do?
	dat.loc[0,['species', 'plot','wgt']]
	
	#What happens when you type the code below?
	dat.loc[[0,10,35549],:]


To do this, we need to provide an index that specifies what part of the data frame we'd like to extract. We can ask for a data value according to the row and column location of the value within the data frame using the `iloc` function: `dat.iloc[row,column]`.


```python
dat.iloc[2,6]
```

which gives **output**
```
'F'
```

Remember that Python indexing begins at 0. So, the index location [2, 6] selects the element that is 3 rows down and 7 columns over in the DataFrame. 

