# Data Structure Notes

------------

1. __What is a Matrix?__
   * Mathematically, matrix is a representations of numbers, symbols, or expressions in a 2-Dimensional Array.

   * In Computer Science, especially with Python, we can start to create a data structure that has values in rows and columns, much like a table, by utilizing a list within a list. There are external libraries/modules that can be imported into your python program to help this process; however, we will be constructing them with just the standalone python version.

   * This is a fundamental concept in mathematics especially for Calculus, Vectors, and Linear Algebra.

     Mathematical Matrix Diagram

      ![matrix_fig01](https://user-images.githubusercontent.com/66268852/233755591-4dbd6746-251c-459a-8891-0186c3762ebb.png)
     
Matrix A in Python 3

```  Python Script

matrix_A = [
    [1, 2, 3, 4],
    [5, 6, 7, 8]
]

# Accessing Matrix A
print('Row 1: %s' % matrix_A[0]) # Recall: Indexing starts at zero in Python
print('Value at Row 2 Column 2: %s' % matrix_A[1][1])
Row 1: [1, 2, 3, 4]

```


2. __List Comprehension in Python 3__
    
    List Comprehension is a concise method to create list in Python 3.

    This technique is commonly used when:

      * The list is a result of some operations applied to all its items
      * It is a made from another sequence/iterable data
      * The list is member of another list/sequence/iterable data that satisfies a certain condition
      * This is where the lambda function would be used, but… we will learn the other way for readability. We will definitely talk about lambda functions in our Functional Programming Unit

   1. List Comprehension Example 1
   
    We are to create a list which squares all the numbers from [0,10)

``` Python
# Old Method
squares = []
for i in range(10):
    squares.append(i ** 2)

print('Our result: %s' % squares)
```

  Our result: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

``` python
# List Comprehension

squares = [i**2 for i in range(10)]

print('Our new result: %s' % squares)
```
  Our new result: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
3. __How Does it Work__
    List comprehension consists of:

      * A Square Bracket containing an expression that describes the list

      * One or more For clause to explain its members

      * Then a zero or more if clauses depending on the complexity of the list
      
      * Examine: [i**2 for i in range(10)]

-- i**2 for i in range(10) --> is the expression that describe the list
-- i**2 describes each item in the list
-- i is taken from the for clause
-- for i in range(10) describes where i comes from
List Comprehension Example 2
Create the list: [[1, 3], [1, 4], [2, 3], [2, 1], [2, 4], [3, 1], [3, 4]]
From
A = [1,2,3]
B = [3,1,4]

  *By using list comprehension*

``` python
# Solution
a = [1,2,3]
b = [3,1,4]

result = [[x, y] for x in a for y in b if x != y]
print(result)
```

[[1, 3], [1, 4], [2, 3], [2, 1], [2, 4], [3, 1], [3, 4]]
Explanation:

Each item of our list has to be a list of two values; therefore, each item is described as [x, y]

There are two for clauses because we are create a list from two sources
-- x comes from a
-- y comes from b

There is a condition to our item --> x != y
-- Therefore, as long as the condition x != y is true, we will add the item described as [x,y] to our resulting list

__List Comprehension Example 3__

Use list comprehension to turn a 2D array called vec to a single list

vec = [[1,2,3], [4,5,6], [7,8,9]]
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]

``` Python
# Solution

vec = [[1,2,3], [4,5,6], [7,8,9]]

result = [value for row in vec for value in row]
print('Vec as a single list of values: %s' % result)
```

  * Vec as a single list of values: [1, 2, 3, 4, 5, 6, 7, 8, 9]
 Explanation

  * Vec is an example of a matrix in Python 3 by using list of lists

  * To grab each value one by one from the rows we must do the following in order:
    1. Explain what each item in the list comprehension is going to be ... in our case --> "value"
    2. To now access where value is, define where it comes from ... in our case --> "row";
        therefore, for row in vec
    3. Finally we construct our last for clause to denote that value comes from the row.
    
    
__Map & Filter In Python 3__

In this note, we will cover some useful built-in functions to help us extend our list comprehension capabilities. These two functions will also be revisited when we do functional programming and lambda functions.

## The Map Function

The idea of a map function is to apply a function to an iterable data.

Formatting:

```python
map(function_name, sequence)
```
  
  * function_name: any function (built-in or self-made) that returns a desired value of choice
  
  * sequence: any iterable data type

  Example:
  
 ```Python
 def square(num):
    ''' squares the given num argument '''
    return num ** 2

array = list(range(1,11))
square_array = list(map(square, array))

print('Original Array:', array)
print('Array Squared:', square_array)
```
  
  One thing to note about the map function is that it doesn’t return a specific data type, but rather, a python iterable data. Therefore, after we apply the map function, we just execute a list function on it.

   Example 2:

``` Python 
def upper(x):
    ''' upper() turns string x into its uppercased counterpart '''
    return x.upper()

word = 'hello world!'
upper_word = ''.join(list(map(upper, word)))

print(word)
print(upper_word)

# simpler way:
print(word.upper())
```

In example 2, we are doing a lot of unnecessary work to make our original word variable uppercased. This is an example of how you shouldn’t use map() for every little change you want to a string.

This also applies to all data structures that have methods. You don’t want to use methods with 'map', since there is a high probability that there is already a method for what you might want to do.

__Filter Function__

The idea of the filter function is to filter out items from a data set that meet a certain condition.

Formatting:

``` Python
filter(bool_returning_function, sequence)
```

function: The function name we provide for filter() must return a boolean value and should also be able to handle the items inside the sequence as its arguments
sequence: any iterable data type

Example 3:

``` Python
def isOdd(x):
    ''' isOdd() returns True if x is odd.'''
    return x % 2 != 0

array = list(range(1,101))
odds = list(filter(isOdd, array))

print('Odd Numbers from 1 to 100:', odds)
```

It is true that this can be done differently, but this was a simplistic use of filter to show we can filter out variables that satisfy a condition… aka the condition is True.

__Example Problem: List of Palindromic Numbers__

    *Our goal in this example program is to create a list of palindromic numbers (numbers that are palindromes) from 1 to 10,000.
``` Python
def isPalindrome(x):
    ''' isPalindrome returns True if string X is a palindrome.'''
    return x == x[::-1]

array = list(range(1,10000))

palindromic_numbers = list(map(int, filter(isPalindrome, map(str, array))))
print('Palindromic Numbers from 1 to 10,000', palindromic_numbers)
```

Function Composition Breakdown:

  1. String version of the array -> map(str, array)
  2. Filter out the palindrome -> filter(isPalindrome, string version of the array)
  3. Remap all values back to integers -> map(int, palindromes)




__What are Tuples?__
 
 Strings and Lists are basic iterable data types that are very similar with key differences:

    * Strings only allow alphanumeric characters and special symbols to represent text
    
    * Lists allow all data types as its items/members

    * Strings are immutable whereas Lists are mutable

  These significant differences cause a headache when you require the following data structure:

    1. It must be immutable
    2. It must allow different datatypes as items
    3. It must be iterable
    4. It must be nestable (much like a list within a list)
All of these are solved with a data structure called: Tuple.

__How to use Tuples in Python 3__

  * Tuples are declared with parenthesis … aka round brackets
  
  * () is an empty tuple
  
  * (50,) is a singleton tuple; the comma is required
 
  * Tuples are sliceable; therefore, indexable using square brackets

  A singleton is an iterable data structure with only single item.

  Example: 
```Python
tup = ('C', 'Java', 'Python')
empty_tup = ()
single_tup = ('Park',)

print(tup)
print(empty_tup)
print(single_tup)
```
  Tuple Operators
```Python
# Concatenation: Joining two tuples
a = (1, 2, 3)
b = (4, 5, 6)
concat_result = a + b
print('a+b:', concat_result)

# Repetition: Repeating a tuple multiple times
c = ('Hi!',)
repet_result = c * 3
print('c*3', repet_result)

# Membership: Check if a value exists in a tuple
d = a + b + c
print('d:', d)
print('\'Hi!\' in d:', 'Hi!' in d)
print('7 in d:', 7 in d)

# Output:
# a+b: (1, 2, 3, 4, 5, 6)
# c*3 ('Hi!', 'Hi!', 'Hi!')
# d: (1, 2, 3, 4, 5, 6, 'Hi!')
# 'Hi!' in d: True
# 7 in d: False
```

  Tuples are Iterable, Indexable, and Sliceable
``` Python
example = ('C', 'Java', 'Python', 'C#', 'JavaScript')

# Iteration
print('Tuple example items:')
for language in example:
    print(language)
print('--')

# Indexing
print('Index 1:', example[1])
print('Last Value:', example[-1])

# Slicing
print('Backwards:', example[::-1])
print('Every other:', example[::2])
print('From 1 to end:', example[1:])
print('From 1 to 3:', example[1:3])

# Output:
# Tuple example items:
# C
# Java
# Python
# C#
# JavaScript
# --
# Index 1: Java
# Last Value: JavaScript
# Backwards: ('JavaScript', 'C#', 'Python', 'Java', 'C')
# Every other: ('C', 'Python', 'JavaScript')
# From 1 to end: ('Java', 'Python', 'C#', 'JavaScript')
# From 1 to 3: ('Java', 'Python')
```

  Built-in Functions with Tuple
``` Python 
# Iteration
example = ('C', 'Java', 'Python', 'C#', 'JavaScript')

print('Tuple example items:')
for language in example:
    print(language)
print('--')

# Indexing
print('Index 1:', example[1])
print('Last Value:', example[-1])

# Slicing
print('Backwards:', example[::-1])
print('Every other:', example[::2])
print('From 1 to end:', example[1:])
print('From 1 to 3:', example[1:3])
```
  Built-in Functions with Tuples
``` Python
example = ('C', 'Java', 'Python', 'C#', 'JavaScript')

print('Length:', len(example))
print('Minimum value:', min(example))
print('Maximum value:', max(example))
print('--')

word = 'Hello'
array = [1, 2, 3, 4]
array_array = [[1], [2, 3], [4]]

print('String to Tuple:', tuple(word))
print('List to Tuple:', tuple(array))
print('2D array to Tuple:', tuple(array_array))
print('--')

array_array[0][0] = 'p'
print(array_array)
```

  Tuple Comprehension
``` Python
# Tuple of Even values from 1 to 100
even_tup = tuple(i for i in range(1, 101) if i % 2 == 0)

print(even_tup)
```

  Tuple & Python: Packing and Unpacking
``` Python
# Packing
var_1 = 2
var_2 = 3
var_3 = 5

prime = var_1, var_2, var_3

print('Packed prime values:', prime)

# Unpacking and Repacking
fib = (0, 1, 1, 2, 3, 5, 8)

fib_0, fib_1, fib_n = fib[0], fib[1], fib[2:]
print('fib_0:', fib_0)
print('fib_1:', fib_1)
print('fib_n:', fib_n)

```

Tuples are an essential data structure in Python that allow for the storage of immutable, heterogeneous data that can be iterated over, indexed, sliced, and nested. Understanding how to work with tuples can greatly enhance one's Python programming skills.


__Sets in Python 3__

    A set is an unordered collection with no duplicate elements in Python 3. It is a mathematical way to describe a collection of different unique objects. By following the operations and characteristics of the mathematical set, we can utilize such a data structure in our Python code.

  Using Sets in Python 3
``` Python
# Set definition examples:
example_set1 = {1, 2, 3}
example_set2 = {'h','e','l','l','o'}

print('example_set1:', example_set1)
print('example_set2:', example_set2) # Notice there is only 1 'l'; Also notice the order of the values outputted
print('--')

singleton_set = {7}
empty_set = set() # this is because {} is reversed for a different feature in python 3.

print('Singleton:', singleton_set)
print('Empty Set:', empty_set)
```

  Basic Built-in Functions w/ Sets

``` Python
# Basic Built-in Functions w/ Sets

example_set = set('hello') # set() turns an iterable into a set
print('example_set:', example_set)
print('--')

print('Number of Values:', len(example_set)) # length function
print('Minimum Value:', min(example_set)) # min function
print('Maximum Value:', max(example_set)) # max function
print('--')

# tuple to set
tup = (2,3,5,7)
print('tup to set:', set(tup))

# list to set
array = ['orange']*2 +  ['watermelon', 'apple'] + ['kiwi'] * 10
print('Original Array:', array)
print('list to set:', set(array))
```

  Basic Membership Operators

``` Python 
# Membership Example
example_set = set('hello')

print("Membership of: \'h\'", 'h' in example_set)
print("Non-Membership of: \'z\'", 'z' not in example_set)
```

  Accessing Values in a Set

``` Python

# Iteration of a Set
example_set = {2,3,5,7,11,13}

for v in example_set:
    print('Values of example_set:', v)
```

  Python 3 Sets are mutable: Adding and Removing Values
``` Python
# Adding and Removing Values
languages = set() # empty set initialization

programming_languages = ['C', 'C#', 'Java', 'Python', 'HTML', 'CSS', 'JavaScript', 'Haskell']

for item in programming_languages:
    languages.add(item) # .add() method adds an item to a set

print('Languages set:', languages)
print('--')

languages.discard('HTML') # looks for the target value, if found, it will remove from the set
print('HTML deleted:', languages)

languages.remove('CSS') # remove can be used to delete a value;
# only difference is it will raise an error if the target is not found
print('CSS deleted:', languages)

random_remove = languages.pop() # .pop() method deletes a random value and return the value ... not recommended
print('Randomly Removed value:', random_remove)

languages.clear() # .clear() will empty out a set : output is set()
print('Empty languages:', languages)
```

   Powering Up Sets: Set Operators
      
      * Union
```Python
# Union Example:
set1 = set('hello')
set2 = set('world')

result = set1 | set2 # | is the union operator ... all the members of both set are combined to a single set
# Recall that: there are no duplicates
print('set1 union set 2:', result)
```
    
    * Intersection
``` Python
# Intersection Example:
set1 = set('hello')
set2 = set('world')

result = set1 & set2 # & is the intersection operator ... only the common members of both sets are combined into a single set
print('set1 intersection set 2:', result)
```
    * Difference
``` Python
# Difference Example:
set1 = set('hello')
set2 = set('world')

result = set1 - set2 # - is the difference operator ... the result contains the members of set1 that are not in set2
print('set1 difference set 2:', result)
```
    * Symmetric Difference
``` Python
# Symmetric Difference Example:
set1 = set('hello')
set2 = set('world')

result = set1 ^ set2 # ^ is the symmetric difference operator ... the result contains members of set1 and set2, but not those in both sets
print('set1 symmetric difference set 2:', result)
```
    * Subset and Superset
``` Python
# Subset and Superset Example:
set1 = {1, 2, 3}
set2 = {1, 2, 3, 4, 5}

print('set1 is subset of set2:', set1.issubset(set2)) # True if all elements of set1 are in set2
print('set2 is superset of set1:', set2.issuperset(set1)) # True if all elements of set1 are in set2
```

     * Set Comprehensions
``` Python 
# Set Comprehensions Example:
numbers = [1, 2, 3, 3, 4, 5, 6, 6, 7, 7, 8, 9]

unique_squares = {x ** 2 for x in numbers} # set comprehension to find unique square values
print('Unique Squares:', unique_squares)
```
  
  Ending Notes on Sets for Python:
    
    * Sets aren’t sliceable nor indexable
    
    * Sets cannot have sets inside them
    
    * Sets do not have order; nor order of insertion
    
    
    * Sets cannot guarantee that their values will be in order
    
    * Sets do not record a value’s position
 
 
 __Dictionary in Python 3__
 
 A dictionary, also known as an associative array, map, or symbol table, is a data type that stores a collection of (key, value) pairs, such that each possible key appears at most once in the collection.

 Common Operations:
  1. Adding a pair
  2. Removing a pair
  3. Modify an existing pair
  4. Lookup of a value associated with a particular key
  Note: This concept is an introduction to similar concepts like hash table and search trees.

*Defining a Dictionary in Python 3*:

Dictionaries use {} like sets; however, their individual item format is very different. Each item in a dictionary is a pair of key and value.
``` Python
# Dictionary Example
sammy = {
    'username': 'sammy',
    'online': True,
    'followers': 42
}

# There are 3 items: each with their unique addresses and value
# Accessing
print('Sammy dict:', sammy)
print('Username:', sammy['username'])
print('Online Status:', sammy['online'])
print('Follower Count:', sammy['followers'])
```

*Dictionary Properties*

  Each item in a dictionary is a key, value pair.

  Keys

  Keys are unique addresses for a dictionary value’s location.

  Key Properties:

    * Must be immutable (strings, numbers, tuples, frozenset)
    * Unique; therefore, two same key values cannot exist in a single dictionary
    * The newest created item with a duplicate key supersedes the previous declaration
  
  Values

  Values of a dictionary within a key can be any data type.

*Updating a Dictionary*
1. We can modify existing values by referencing the key.
2. We can add new values to a dictionary by creating a new key.
3. We can overwrite a value at an existing key by referencing and recreating the value for it.

``` Python
# Update Example

sammy = {
    'username': 'sammy',
    'online': True,
    'followers': 42
}

sammy['followers'] += 10 # We are adding 10 to the value located at key: 'followers'
sammy['verified'] = True # We added a new value at a new key: 'verified'
sammy['username'] = 'SammySammy'

print('Sammy Dict:', sammy)
```

*Deletion with Dictionary*

  1. We can delete a key hence deleting the value connected to the key.
  2. We can empty out the entire dictionary.
  3. We can delete the dictionary (uncommonly used).

``` Python
# Deletion Example

sammy = {
    'username': 'sammy',
    'online': True,
    'followers': 42
}

del sammy['followers'] # del is a keyword used to help us to execute a removal
print('followers key deleted:', sammy)

sammy.clear() # {} is considered an empty dict
print('emptying out a dictionary', sammy)
print('--\n\n')

del sammy
print('Deleting sammy, should create an error when referenced again', sammy)
```

Built-in Functions’ Interactions with Dictionaries
``` Python
# Built-in Function Interactions

sammy = {
    'username': 'sammy',
    'online': True,
    'followers': 42
}

print('Size of sammy dict:', len(sammy))
print('Largest Key:', max(sammy))
print('Smallest Key:', min(sammy))
print('Dict to string:', str(sammy))
print('Dict to list:', list(sammy))
```

Duplicate a Dictionary and Copy Keys Only
``` Python
# Duplicate a Dictionary

sammy = {
    'username': 'sammy',
    'online': True,
    'followers': 42
}

sammy_copy1 = sammy.copy()
sammy_copy2 = sammy

sammy['verified'] = True

print('sammy_copy1:', sammy_copy1)
print('sammy_copy2:', sammy_copy2)
print('--')

# Duplicate keys only

tammy = tammy.fromkeys(sammy) # Notice that all key's values are None ... aka empty

print('tammy dict:', tammy)
```

Dictionary Methods
Dictionaries have a good set of methods for us to use.

Let A and B be dictionaries:

1. A.keys() –> Returns a sequence of keys/addresses in A
2. A.values() –> Returns a sequence of item values in A
3. A.items() –> Returns a sequence of key,item pairs in A
4. A.get(address) –> Returns the item value at address
5. A.update(B) –> Extends A with the dictionary of key,value pairs of B

``` Python
# Dictionary Method Examples

sammy = {
    'username': 'sammy',
    'online': True,
    'followers': 42
}

sammy_hidden = {
    'pwd' : 'qwerty',
    'location' : 'Toronto, Ontario'
}

# printing all the keys of a dict
print('Sammy Dict Keys:', sammy.keys()) # notice how it prints

sammy_keys = list(sammy.keys()) # we can listify the .keys() returned
print('List of sammy_keys', sammy_keys)
print('--')

# printing all the values of a dict
print('Sammy Dict Values:', sammy.values())
print('Sammy Dict Values
```

   
