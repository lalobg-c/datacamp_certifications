# Python Toolbox

## Using iterators in PythonLand

### Iterators and iterables
* Iterator
- An iterable is an object with an associated iter() method. For example: lists, strings, dictionaries, file connections.
- Applying iter() to an iterable creates an iterator.

* Iterable
- Produces next value with next()

Example:
```python
   word = 'Da'
   it = iter(word)
   next(it) #'D'
   next(it) #'a'
   next(it) # Throws a StopIteration error

   word = 'Data'
   print(*it) # D a t a
```

### Some functions

* enumerate()
```python
list_name = [...]
e = enumerate(list_name)
print(type(e)) # <class 'enumerate'> This object is an iterable.

for index, value in enumerate(list_name, start = n):
    print(index, value)
```

* zip()
```python
list_1 = []
list_2 = []
z = zip(list1, list2) # Creates an iterator of tuples.
type(z) # <class 'zip'>
z_list = list(z)

zip_object = zip(list1, list2,...)
# unpack the zip:
print(*zip_object)
```

### Too much data
- Load data in chunks.
- It can be done with pandas.
    - specify the size: chunksize
    ```python
        import pandas as pd
        result = []
        for chunk in pd.read_csv('data.csv', chunksize=1000)
            result.append(sum(chunk['x']))
        total = sum(result)

        # another way of doing it:
        total = 0
        for chunk in pd.read_csv('data.csv', chunksize=1000)
            total += sum(chunk['x'])
    ```
///////////////////////////////////////////////////////////////////

## List comprehensions and generators
* List comprehensions
- Populate a list with a for loop:
    ```python
    nums = [12, 8, 21, 3, 16]
    new_nums = []
    for num in nums:
        new_nums.append(num+1) # [13, 9, 22, 4, 17] 
    ```
- The previous can be done in a single line:
    ```python
    nums = [12, 8, 21, 3, 16]
    new_nums = [num+1 for num in nums]
    # This is called a list comprehension.
    # Other example:
    result = [num for num in range(11)]
    #--> [0,1,2,3,...10]

    # Nested
    nested_lists = [(num1, num2) for num1 in range(0,2) for num2 in range(6,8)
    #--> [(0,6), (0,7), (1,6), (1,7)]]
    ```
* Advanced comprehensions
- Conditionals in comprehensions
    ```python
    [num ** 2 for num in range(10) if num % 2 == 0]
    # --> [0, 4, 16, 36, 64]

    [num ** 2 if num % 2 == 0 else 0 for num in range(10)]
    # --> [0, 0, 4, 0, 16, 0, 36, 0, 64, 0]
    ```

- Dictionary comprehensions
    ```python
    pos_neg = {num: -num for num in range(9)}
    # --> returns a dictionary
    ```

* Introduction to generator expressions
- A generator is created in a similar way as comprehensions:
    ```python
    # e.g.1
    (2 * num for num in range(10))

    # The difference with [] is that () creates a generator object, which does not store data in memory, instead, it creates an object which can be iterated to produce elements of the list as required.

    # e.g.2
    result = (num for num in range(6))
    for num in result:
        print(num) # 0 1 2 3 4 5

    print(list(result)) # --> list

    # Lazy evaluation
    print(next(result)) # 0
    print(next(result)) # 1
    print(next(result)) # 2 ...

    ## e.g.3
    [num for num in range(10**1000000)] # impossible to create
    (num for num in range(10**1000000)) # this can be done.
    ```

- Conditionals in generator expressions
    ```python
    # e.g.1
    even_nums = (num for num in range(10) if num % 2 == 0)

    # e.g.2
    # Generator functions
    def num_sequence(n):
        """Generate values from 0 to n"""
        i = 0
        while i < n:
            yield i
            i += 1
    result = num_sequence(5)
    ```

///////////////////////////////////////////////////////////////////

## Bringing it all together!

* World bank data
    - Contains data on world economies (217) for over half a century:
        - Population
        - Electricity consumption
        - CO2 emissions
        - Literacy rates
        - Unemployment
        - Mortality rates



