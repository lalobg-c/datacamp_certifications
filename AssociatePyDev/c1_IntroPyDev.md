# Introduction to Python

- Python is a high-level programming language. Meaning, it resembles natural language. But it is slow compared to other languages, like C or Java.
- Python is a dynamically written language, meaning we do not need to tell what data type the variable is.
- Python can be used to develop a lot of things, from web apps to machine learning.

- Variable name is case sensitive.

## String methods
    ```python
    str_variable.method()
    str.replace("string1", "string2")
    str.lower()
    str.upper()
    multiline_string = """This
                    would be a multiline
                    string. For larger texts.
                    """
    ```

## Lists
- Store multiple values of any data type in a single variable.
- Lists are zero index based.
    ```python
    namelist = []
    namelist[index] #for subsetting.
    namelist[start:last+1] #for subsetting from start to last.
    namelist[i:] #access all elements from the index i onwards.
    namelist[:i] #access the first i elements.
    namelist[::i] #access every other element in the list.
    namelist[i::j]
    namelist[-1] # Get the last element.
    ```

## Dictionaries
- Is a data structure consisting of key-value pairs.
    ```python
    products_dict = {"key_string": value, ... }
    ```
- Dictionaries are ordered. Subset is done using the key.
    ```python
    products_dict.values()
    products_dict.keys()
    products_dict.items()
    products_dict["new_key"] = value
    products_dict["existing_key"] = new_value
    ```

## Sets and tuples
- A set contains unique data. Its values cannot be changed.
    ```python
    set_name = {} # No : implies it is a set.
    set_name = set(list_name) # cast a list to a set. 
    sorted(set_name) # returns a list ordered by letter.
    ```
- A set has no indices. Subset is not possible.


## Tuples
- Immutable, cannot be changed. No adding, removing or chaging values.
- Tuples are ordered. They can be subset by index.
    ```python
    tuple_name = (...)
    ```

## Conditionals
- Symbols: == != < > >= <= =>
- Statements: if, if-elif, if-elif-else

## Loops
### For loops
    ```python
    for value in sequence:
        action
    # For dictionaries:
    for key, val in dictionary_name.items():
        print(key, val)
    # or
    for key in dictionary_name.keys():
    for val in dictionary_name.values():
    # other example
    for i in range(start, end + 1):
        print(i)
    ```

### While loops
    ```python
        while condition:
            action
        # Example 1:
        stock = 10
        num_purchases = 0
        while num_purchases < stock:
            num_purchases += 1
            print(stock - num_purchases)
            # break can be used to terminate the loop.
            # it can also be used in for loops.

            # Example 1.1:
            if stock - num_purchases > 7:
                print("Plenty stock")
            elif stock - num_purchases > 3:
                print("Some stock")
            elif stock - num_purchases != 0:
                print("Low stock")
            else:
                print("no stock!")
    ```

## Build a workflow
- not
- and
- or
### Appending
    ```python
    # Example:
    list_name = []
    for key, val in dictionary_name.items():
        if val >= number:
            list_name.append(key)
    ```
