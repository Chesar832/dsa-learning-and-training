# Hash maps/tables

## What is it?
**Hashing** is the process which takes a value and transform it into another value. Usually the result is a fixed-size number which is computationally easier to work with (more than the original key).

The idea is to distribute pairs of key and values to an array of buckets where each key is represeted by an index as result of the hasing function applied to it.

![img](https://media.datacamp.com/legacy/v1706003255/image3_8dd5da6cf2.png)

## Why?
This structure comes with Python as `dictionary` and it's useful because facilitates the accessing to values with less complexity than a list being O(1) instead of O(n).

# Visualization
![img](https://www.boardinfinity.com/blog/content/images/2023/03/HashMap-in-Python.png)

## Supported operations
- `list(d)`: Return a list of all the keys used in the dictionary d.
- `len(d)`: Return the number of items in the dictionary d.
- `d[key]`: Return the item of d with key key. Raises a KeyError if key is not in the map.
- `d[key] = value`: Set d[key] to value.
- `del d[key]`: Remove d[key] from d. Raises a KeyError if key is not in the map.
- `key in d`: Return True if d has a key *"key"*, else False.
- `clear()`: Remove all items from the dictionary.
- `get(key, default=None)`: Return the value for key if key is in the dictionary, else default. If default is not given, it defaults to None, so that this method never raises a KeyError.
- `pop(key[, default])`: If key is in the dictionary, remove it and return its value, else return default. If default is not given and key is not in the dictionary, a KeyError is raised.
- `keys()`: list all the keys of the dict.
- `values()`: list all the values of the dict.
- `items()`: returns all the pairs of keys and values of the dict.

## Time complexity of the operations
| Operation                | Average Case | Why?                                        |
|--------------------------|--------------|---------------------------------------------|
| `list(d)`                | O(n)         | Copies all keys into a new list             |
| `len(d)`                 | O(1)         | Dictionary tracks size internally           |
| `d[key]`                 | O(1)         | Direct access via hash function             |
| `d[key] = value`         | O(1)         | Inserts using computed hash index           |
| `del d[key]`             | O(1)         | Finds and removes key using hash            |
| `key in d`               | O(1)         | Checks hash index for key presence          |
| `clear()`                | O(n)         | Removes all elements one by one             |
| `get(key, default)`      | O(1)         | Uses hash to fetch key, returns default     |
| `pop(key[, default])`    | O(1)         | Same as `get` plus delete                   |
| `keys()`                 | O(n)         | Iterates through and returns all keys       |
| `values()`               | O(n)         | Iterates through and returns all values     |
| `items()`                | O(n)         | Iterates and returns all key-value pairs    |

## Implementation from scratch



## Additional features of the `dict`
- **Dictionaries are mutable:** It's a mutable data structure, so we can add, remove or modify the values of the pairs stored in it.
- **Keys are immutable:** That means that keys are always data types that cannot be changed. In other words, dictionaries will only allow data types that are hashable, like strings, numbers, and tuples. On the contrary, keys can never be a mutable data type, such as a list.
- **Keys are unique:** Keys are unique within a dictionary and can not be duplicated inside a dictionary. If it is used more than once, subsequent entries will overwrite the previous value.

## `Defaultdict`
Every time you try to access a key that is not present in your dictionary, Python will return a KeyError. A way to prevent this is by searching for information using the `.get()` method. However, an optimized way to do that is by using `Defaultdict`, available in the module `collections`. `Defaultdict` and dictionaries are almost the same. The sole difference is that `Defaultdict` never raises an error because it provides a default value for non-existent keys.

```python
from collections import defaultdict 

# Defining the dict 
capitals = defaultdict(lambda: "The key doesn't exist") 
capitals['Madrid'] = 'Spain'
capitals['Lisboa'] = 'Portugal'
  
print(capitals['Madrid']) 
print(capitals['Lisboa']) 
print(capitals['Ankara']) 

# Returns
>> Spain
>> Portugal
>> The key doesn't exist 
```




