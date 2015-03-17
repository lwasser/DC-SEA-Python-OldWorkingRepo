#VARIABLES STUFF

For example,

```python
weight_kg = 55
```

When we gave variable a value, we can print it:

```python
weight_kg
```

which gives **output**

```
55
```

and manipulate whit it, for example multiply it:

```python
3.5*weight_kg
```

which gives **output**

```
192.5
```

We can also change a variable's value by assigning it a new one and print out the information using 'print' to add text and values together:

```python
weight_kg = 52
print "person lost some weight and now weights", weight_kg
```

which gives **output**

```
person lost some weight and now weights  52
```

If we imagine the variable as a sticky note with a name written on it, assignment is like putting the sticky note on a particular value. This means that assigning a value to one variable does not change the values of other variables. For example, let's store the animal's weight in pounds in a variable:

```python
weight_lb = 2.2 * weight_kg
print "animal's weight in kilograms:", weight_kg, "and in pounds:", weight_lb
```

which gives **output**

```
animal's weight in kilograms: 52 and in pounds: 114.4
```

and then change variable weight_kg

```python
weight_kg = 80
print "animal weight in kilograms:", weight_kg, "but in pounds is still", weight_lb
```

which gives **output**

```
animal's weight in kilograms: 80 but in pounds is still 114.4
```

#### Updating a Variable

Since variable `weight_lb` doesn't "remember" where its value came from, it isn't automatically updated when variable `weight_kg` changes. This is different from the way spreadsheets work.

#### Challenges

Draw diagrams showing what variables refer to what values after each statement in the following commands:

```python
mass = 47.5
age  = 122
mass = mass * 2.0
age  = age - 20
```

**What is your answer?**


Variables also could be vectors or matricies.

```python
vector = [0,2.5]
matrix = [[0,2],[0,1]]
print "vector =", vector, "matrix =", matrix
```

which gives **output**

```
[0, 2.5] [[0, 2], [0, 1]]
```



Therefore, we can also add to variable that are vectors, and update them by making them longer. 
For example, if we are creating a vector of animal weights, we could update that vector using its iternal `.append` method. 

```print
weights = [100]
print weights
weights.append(80)
print weights
```

which gives **output**

```
[100]
[100, 80]
```