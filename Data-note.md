# Data Structure Notes

------------

1. __ What is a Matrix? __
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
    
    
 
 
 4. Map & Filter In Python 3
In this note, we will be covering some useful built-in functions to help us extend our list comprehension capabilities.

These two functions that we learn will also be revisited when we do functional programming and lambda functions.

The Map Function
The idea of a map function is to apply a function to an iterable data.

Formatting:

python
Copy code
map(function_name, sequence)
function_name: any function (built-in or selfmade) that returns a desired value of choice
sequence: any iterable data type
Example:

python
Copy code
def square(num):
    ''' squares the given num argument '''
    return num ** 2

array = list(range(1,11))
square_array = list(map(square, array))

print('Original Array:', array)
print('Array Squared:', square_array)
One thing to note about the map function is that it doesn’t return a specific data type, but rather, an python iterable data. Therefore, after we apply the map function, we just execute a list function on it.

Example 2:

python
Copy code
def upper(x):
    ''' upper() turns string x into its uppercased counter part '''
    return x.upper()

word = 'hello world!'
upper_word = ''.join(list(map(upper, word)))

print(word)
print(upper_word)

# simpler way:
print(word.upper())
In example 2, we are doing a lot of unnecessary work to make our original word variable uppercased. This is an example of how you shouldn’t use map() for every little changes you want to a string.

This also applies to all data structure that has methods. You don’t want to use methods with map, since there is a high probability that there is already method for what you might want to do.

Filter Function
The idea of the filter function is to filter out items from a data set that meets a certain condition.

Formatting:

python
Copy code
filter(bool_returning_function, sequence)
function: The function name we provide for filter() must return a boolean value and should also be able handle the items inside the sequence as its arguments
sequence: any iterable data type
Example 3:

python
Copy code
def isOdd(x):
    ''' isOdd() returns True if x is odd.'''
    return x % 2 != 0

array = list(range(1,101))
odds = list(filter(isOdd, array))

print('Odd Numbers from 1 to 100:', odds)
It is true that this can be done differently, but this was a simplistic use of filter to show we can filter out variables that satisfy a condition… aka the condition is True.

Example Problem: List of Palindromic Numbers
Our goal in this example program is to create a list of palindromic numbers (numbers that are palindromes) from 1 to 10,000.

python
Copy code
def isPalindrome(x):
    ''' isPalindrome returns True if string X is a palindrome.'''
    return x == x[::-1]

array = list(range(1,10000))

palindromic_numbers = list(map(int, filter(isPalindrome, map(str, array))))
print('Palindromic Numbers from 1 to 10,000', palindromicNumbers)
Function Composition Breakdown:

string version of the array --> map(str, array)
filter out the palindrome --> filter(isPalindrome, string version of the array)
remap all values back to integers --> map(int, palindromes)
turn the mapped integers iterable back inside


