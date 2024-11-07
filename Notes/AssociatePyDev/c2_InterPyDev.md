# Intermediate Python for Developers

## The Python Ecosystem
- Functions
- Modules
- Packages

### Some built-in functions
    ```python
    max(list_name)
    min(list_name)
    sum(list_name)
    round(number, decimals)
    # Call a function within a function
    round(sum(list_name))

    # len counts the number of elements
    len(list_name)
    len("a string")
    len(dictionary)

    # another 
    sorted(list_name)
    sorted("a string")

    # To get information about a function
    help(function_name)
    ```

## Working with functions
    ```python
    def function_name(parameters):
        indented code
        return
    # example
    def average(values):
        # Next line sets the documentation of the function, which is accessed by
        # the dunder_doc attribute. See below.
        """Find the mean in a sequence of values and round to two decimal places
        It is possible to do a multiline documentation
        Like this
        Args:
            values (list): A list of numeric values
        Returns:
            rounded_average (float) ...

        """
        average_value = sum(values) / len(values)
        return round(average_value, 2)
    average(list_name)
    ```
- Functions and methods have two types of arguments: positional and keyword.
    - help(name_function) to get more information about a function.

    ```python
    def average(values, rounded=False):
        if rounded == True:
            average_value = sum(values) / len(values)
            rounded_average = round(average_value, 2)
            return rounded_average
        else:
            average_value = sum(values) / len(values)
            return average_value

    average(list_name, False)
    average(list_name, True)

    function_name.__doc__ # dunder_doc attribute. To access the documentation.
    ```
- Arbitrary and arbitrary keyword arguments:
    ```python
    def average(*args):
    # example:
    average(15, 29, 4, 13, 11, 8) # 13.33
    average(*[15, 29], *[4, 13], *[11, 8]) # 13.33


    def average(**kwargs):
        average_value = sum(kwargs.values) / len(kwargs.values)
        rounded_average = round(average_value, 2)
        return rounded_average

    average(a=15, b=29, c=4, d=13, e=11, f=8) # 13.33
    average(**{"a":15, "b":29, "c":4, ...}) # 13.33
    average(**{"a":15, "b":29}, **{}, **{}, ...)
    ```

## Lambda functions and error handling
- A function that does not need a name.
- Return statement is not needed.
    ```python
    lambda arguments: expression

    (lambda x: sum(x) / len(x))[3, 6, 9]
    average = lambda x: sum(x) / len(x)
    average([values])

    (lambda x, y: x**y)(2, 3) # 8

    # apply a lambda to all elements in an iterable
    names = ["a", "b", "c"]
    capitalize = map(lambda x: x.capitalize(), names) # This is a map object
    # convert it to a list.
    list(capitalize)
    ```

### Handling error
- try-except
- raise

    ```python
    def average(values):
        try:
            average_value = sum(values) / len(values)
            return average_value
        except:
            print("average() accepts a list or set. Please provide a correct data type.")

    def average(values):
        if type(values) in ["list", "set"]:
            average_value = sum(values) / len(values)
            return average_value
        else:
            raise TypeError("average() accepts a list or set, please provide a correct data type.")

    ```
