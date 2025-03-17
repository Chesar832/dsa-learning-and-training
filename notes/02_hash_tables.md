# Hash maps/tables

## Why?
This structure comes with Python as `dictionary` and it's useful because facilitates the accessing to values with less complexity than a list being O(1) instead of O(n).

## Concepts

**Hashing** is the process which takes a value and transform it into another value. Usually the result is a fixed-size number which is computationally easier to work with (more than the original key).

The idea is to distribute pairs of key and values to an array of buckets where each key is represeted by an index as result of the hasing function applied to it.

![img](https://media.datacamp.com/legacy/v1706003255/image3_8dd5da6cf2.png)

## Features of the `dict`
- **Dictionaries are mutable:** It's a mutable data structure, so we can add, remove or modify the values of the pairs stored in it.
- **Keys are immutable:** That means that keys are always data types that cannot be changed. In other words, dictionaries will only allow data types that are hashable, like strings, numbers, and tuples. On the contrary, keys can never be a mutable data type, such as a list.
- **Keys are unique:** Keys are unique within a dictionary and can not be duplicated inside a dictionary. If it is used more than once, subsequent entries will overwrite the previous value.

## Retrieving data
- `keys()`: list all the keys of the dict.
- `values()`: list all the values of the dict.
- `items()`: returns all the pairs of keys and values of the dict.

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




