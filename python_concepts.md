# Python Basics

## Iterables

Iterables are objects that can be iterated over. Examples of iterables in Python are lists, strings, dictionaries, tuples, and sets.
For any iterable, you can get its length (or size) by calling the method `len`. Here are a few examples: `len([1, 2, 3])`, `len((1, 2, 3))`

### For Loops

In Python we can iterate over iterables using a `for` loop. For example, we can iterate over a list as follows:

```python
lst = [1, 2, 3]
for elem in lst:
	print(elem)
```

The syntax resembles the syntax of foreach loops in other languages. `elem` will be assigned to each element of the list `lst` in turn, and the body of the loop will be executed for each element. The body of the loop is indented, as in if statements.

Alternatively, we may be more interested in iterating over the positions of an index.
A common way to do it, is through the use of a for loop and the `range` function. 
`range` is a function that returns an iterable of numbers. For example, `range(4)` returns the iterable `[0, 1, 2, 3]`.
Its syntax is `range(start, end, step)` where `start` is the first number in the iterable, `end` is the first number that is not in the iterable, and `step` is the difference between two consecutive numbers in the iterable. `start` and `step` are optional, and their default values are 0 and 1 respectively. `end` is mandatory.

Here are a few usage examples of `range`. They are all equivalent and all produce the iterable `[0, 1, 2, 3]`:

- ```range(4)```
- ```range(0, 4)```
- ```range(0, 4, 1)```

Coming back to iterating the list based on the positions, you can do it as follows:

```python
lst = [1, 2, 3]
for i in range(len(lst)):
	print(lst[i]) # by using [i] we're accessing the index `i` of the list `lst`
```

Unlike Java or C, you have very little control on the conditions that allow you to break out of your for-loop cycle! Instead, to achieve the same in Python, you will need to use `if-else` block and `break` statements. Let us see an example, where we're iterating a list of numbers from 1 to 10 and we want to stop iterating when we find the second even number.

```python
# since we want to know the number of odd numbers in the list we're iterating
# we will need to keep that information in a data structure.
# Since we will dynamically update it, we have to choose a mutable type
# (like list, dictionary, or sets). We choose the list.
lst_of_even_numbers = []

for i in range(10): # range(10) returns an iterable [0, 1, ..., 9]
	if i % 2 == 0:  # check if it's even number
		lst_of_even_numbers.append(i)
	
	if len(lst_of_even_numbers) == 2:
		break # stop iterating when this condition is satisfied
	
	print("Iteration", i)
print("We broke free!")
```

### While loops

Instead of for loops, sometimes you'd like to use `while` loops to have more control on the conditions that will break the cycle, without having to use `break`. For example, let us implement the previous example using a `while` loop.

```python
i = 0 
lst_of_even_numbers = []

while i < 10 and len(lst_of_even_numbers) != 2: # range(10) returns an iterable [0, 1, ..., 9]
	if i % 2 == 0:  # check if it's even number
		lst_of_even_numbers.append(i)
	print("Iteration", i)
	i += 1 # it is equivalent to i = i+1
print("We broke free!")
```

## Logical operators `and` vs `&` and `or` vs `|`

Here we will discuss the two logical operators `and` and `or`, as well as explain you the difference between `and` and `&` `or` vs `|`.
If you know other programming languages like Java or C, you can think of the operators `and` and `or` as the equivalent of `&&` and `||`, respectively.

The operators `&` and `|` in Python represent the bit-wise AND and OR operators. This means that before applying these operations, Python transforms the number into their binary representation and applies the AND and OR for each bit. Let us see some examples:

| Expression | Result | Explanation |
| ---------- | ------ | ----------- |
| `4 and 1`    | 1      | AND must evaluate all its arguments to determine whether it is `True` or `False`. Since all non-zero numbers are considered `True`, this expression evaluates every operand and returns the last operand that is True. |
| `4 & 1`      | 0      | `100` and `001` are the binary representation of numbers 4 and 1, the `&` operator execute a bit-wise `AND` which results in the binary representation of `000`. The final decimal representation is therefore 0. |
| `4 or 1`     | 4      |  OR evaluates the least amount of arguments necessary until it finds one that is evaluated to `True`. In this case, the `4` is considered True by default and therefore the result is `True`. |
| `4 | 1`      | 5      | `100` and `001` are the binary representation of numbers 4 and 1, the `|` operator executes a bit wise `OR` on the binary representation. The result is `101`, which is `5` in the decimal base system. |

## Dictionaries

Python dictionaries define 1-to-1 mappings associating different keys with different values. They can be defined in terms of key-value pairs. They are mutable types, which means they can be modified multiple times. They are the equivalent of hashmaps in programming languages like Java. 

The keys of dictionaries are always non-mutable types, like tuples, strings, integers, floats. This means that lists, sets, and dictionaries cannot be used as keys of dictionaries.

### Creating dictionaries

You can create an empty dictionary and assign it to a variable named `example` using any of the expressions below:
- `example = {}`
- `example = dict()`

Alternatively, sometimes you may want to initialize the dictionary with some key-value pairs.
You can do it using any of the equivalent syntaxes:
- `example_non_empty = {key1: value1, key2: value2, ...}`, where the key is always followed by a `:`.

Concrete examples for initializing dictionaries:

```python
example_non_empty_ints = {1: 1, 2: 3}
example_non_empty = {1: "a", 2: 3}
example_non_empty0 = {"a": 0, 2: "a"}
example_non_empty1 = {("a", "b"): 0, 2: ("a", "c")}
```

### Accessing a specific key

Accessing a value in a dictionary can be done through the use of `[]` (square brackets) and by specifying the key, as follows: `example_non_empty[key1]`.

### Other methods on dictionaries

- Iterate over the keys using `.keys()`: `example_non_empty0.keys()` which returns `["a", 2]` for the dictionaries we defined previously.
- Iterate over the values using `.values()`: `example_non_empty0.values()` which returns `[0, "a"]` for the dictionaries we defined previously.
- Iterate over the list of key-value pairs using `.items()`: `example_non_empty0.items()` returns `[("a", 0), (2, "a")]`; and `example_non_empty1.items()` returns `[(("a", "b"), 0), (2, ("a", "c"))]`.

## Tuples

Are mutable types. This means that tuples cannot be dynamically modified after they were created.
You should use them to define iterables whose legth you know it's gonna remain the same throughout your program.
There's no limit to the size of tuples, they can be as big as you'd like.

- Empty tuple: `tuple()`
- Tuple with 1 element: `(1,)`, `("a",)`, `((1, 2, 3),)`
- Tuple with 2 elements: `(1, 2)`, `(“a”, “b”)`, `(“a”, 1)`
- Tuple with 3 elements: `(1, 2, 3)`

You can also create a tuple from an iterable, using the `tuple(iterable)`, where `iterable` is a variable.

If you ever want to assign the individual values of iterables to individual variables, you can do it through what it's called variable unboxing: `var_a, var_b = (1, 2)`, where `var_a` is assigned to value 1 and `var_b` is assigned to value 2.

## DataFrames

You can iterate dataframe based on columns or rows.

- To iterate over rows you should use `df.iterrows()`, which will return `[tuple1, tuple2, tuple3, …, tuple150]`.

Here are a few snippets of code that are useful to iterate over 

```python
for tupl in df.iterrows():
	i, e = tupl # using variable unboxing
	# write your code here
	...
```

```python
for i, e in df.iterrows(): 
	# write your code here
	...
```

## Lists

```python
# create a list
lst = list() # or equivalently lst = []

# append an element to the end of the list
lst.append(1)

# append a list to the end of the list lst
lst = lst + [[1, 2]]
```
