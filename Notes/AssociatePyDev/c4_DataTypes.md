# Data Types in Python

## Fundamental Sequence Data Types
* Introduction and lists
* Meet the tuples
    - Tuples are very much as lists. Its elements can be accessed by an index.
    - Tuples are immutable: it cant add or remove elements from them.
    - Tuples can be unpacked.
    - Tuples are commonly created by zipping lists together with zip():
    ```python
    list(zip(list_1, list_2))
    ```
* Strings
    - Formatted strings: f""
    - Join with strings: "".join()
    ```python
    # Examples

    child_ages = ["3", "4", "7", "8"]
    print(", ".join(child_ages))
    # --> "3, 4, 7, 8"

    print(f"The children are ages {','.join(child_ages[0:3])}, and {child_ages[-1]}.")
    # --> "The children are ages 3, 4, 7, and 8."

    # Matching parts of a string:
    boys_names = ["Mohamed", "Youssef", "Ahmed"]
    print([name for name in boy_names if name.startswith('A')])
    # --> ["Ahmed "]

    "long" in "Life if a long lesson in humility." #--> True
    "life" in "Life is a long lesson in humility." #--> False

    "life" in "Life is a long lesson in humility.".lower() #--> True
    ```

## Dictionaries - The Root of Python
* Using dictionaries
* Altering dictionaries
* Pythonically using dictionaries
* Mixed data types in dictionaries

- Dictionaries hold data in key/value pairs. They can be nested and they are iterables. A dictionary is created using dict() or {}.
- Adding and extending can be done with dict_name['key'] = value. It can also be done with the .update() method (see below).
- The method .items() returns an object which can be iterated. This is the preferred method to iterate over the items of a dictionary.
- The method .keys() returns an object dict_keys with the keys of the dictionary.
```python
# Creating a dictionary
art_galleries = {}
for name, zip_code in galleries:
    art_galleries[name] = zip_code

art_galleries.get('Louvre', 'Not Found')
## --> Returns Not Found is there is no key called 'Louvre'

## Extending dictionary
tuple_list = [(),(),...]
dict_name['key'].update(tuple_list)

## delete a key
del dict_name['key']
dict_name.pop('key')

## .items method
for gallery, phone_num in art_galleries.items():
    print(gallery)
    print(phone_num)

## in operator, returns a boolean
'key_name' in dict_name #--> true if the key exists
```

## Numeric Data Types, Booleans, and Sets
### Numeric data types
- Integers - whole numbers, large numbers.
- Float - fractional amounts, scientific notation.
- Decimal - for precision, currency operations, this type needs to be imported: from decimal import Decimal.

```python
print(0.00001) #--> 1e-05
print(f"{0.00001:f}") #--> 0.000010
print(f"{0.0000001:f}") #--> 0.000000 only 6 decimals with f
print(f"{0.0000001:.7f}") #--> 0.0000001

# Float division
4/2 #--> 2.0

## Floor division
4//2 # --> 2
7//3 #--> 2
```

### Booleans - The logical data type
- True
- False

- Truthy values:
    - 1
    - "String"
    - ['item1', 'item2', ... ]
    - {'key1': 'value', ... }
- Falsey values:
    - 0
    - ""
    - []
    - {}
    - None

### Sets
- Unique values
- Unordered data
- Mutable

- Sets are created from lists: set_name = set(list_name)
- .add() to add new unique values to a set.
- .update() merges in another set or list.
- .discard() safely removes an element from the set.
- .pop() removes and returns an arbitrary element from the set.
- .union() returns a set of all the names.
- .intersection() identifies overlapping data.
- .difference() identifies data present in the set on which the method was used, not in the argument.


## Advanced Data Types
### Counting made easy
- Collections module
- Counter: special dictionary used for counting data, measuring frequency.
    - .most_common() returns the counter values in descending order.

```python
from collections import Counter
obj_name = Counter(dict_name)
```

### Dictionaries of unknown structure - Defaultdict
```python
from collections import defaultdict
eateries_by_park = defaultdict(list)
for park_id, name in nyc_eateries_parks:
    eateries_by_park[park_id].append(name)

# example2
eatery_contact_types = defaultdict(int)
for eatery in nyc_eateries:
    if eatery.get('phone'):
        eatery_contact_types['phones'] += 1
    if eatery.get('websites'):
        eatery_contact_types['websites'] += 1
```

### What do you mean I don't have any class? Namedtuple
- Like a tuple, but with names.
- Each field is available as an attribute of the namedtuple.
```python
from collections import namedtuple
# example
Eatery = namedtuple('Eatery', ['name', 'location', ...., ])
for eatery in nyc_eateries:
    details = Eatery(
                    eatery['name'],
                    eatery['location'],
                    ... )
    eateries.append(details)

for eatery in eateries[:3]:
    print(eatery.name)
    print(eatery.park_id)
    print(eatery.location)
```


### Dataclasses
- Support for default values.

```python
# Define a class
from dataclasses import dataclass

@dataclass
class Cookie:
    name.str
    quantity: int = 0

chocolate_chip = Cookie("chocolate chip", 13)
print(chocolate_chip.name)
print(chocolate_chip.quantity)

#//////////////////////////
# To convert class to dict or tuple:
from dataclasses import asdict, astuple

ginger_molasses = Cookie("ginger molasses", 8)
asdict(ginger_molasses) #--> {}
astuple(ginger_molasses) #--> ()

# /////////////////////////
# For custom properites:
from decimal import Decimal

@dataclass
class Cookie:
    name: str
    cost: Decimal
    quantity: int
    @ property
    def value_of_goods(self):
        return int(self.quantity) * self.cost

peanut = Cookie("peanut butter", Decimal("1.2"), 8)
peanut.value_of_goods #--> Decimal('9.6')

#///////////////////////
# Froze instances - cannot be edited later
@dataclass(frozen=True)
class Cookie:
    name: str
    quantity: int = 0

c = Cookie("chocolate chip", 10)
c.quantity = 15 #--> ERROR
```
