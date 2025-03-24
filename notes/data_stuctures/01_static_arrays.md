
# Arrays

This is a basic but ver important data structure in Python because it allow to store and manipulate each element in a very effective way using a specific position or index.

## Work in memory
When we create an `array` the computer separates a memory block to store all the array elements and its's equal to the sum of each element multiplied by their respective size.

## Indexing
This is very straightforward, Python uses zero-indexed arrays, but the element can also be accessed by a negative indexing which begins with -1, -2 and so on. These negative indexes give access with and order from the last elememt to the first one.

## Accessing elements
We can access elements of the arrays using the indexes, just like this:


```python
# example of accessing elements
array[0] # first element
array[1] # second element
array[-1] # last element
```

The access of elements through indexes has a constant **time complexity of** $O(1)$ because each element is known with its respective index.    

## Manipulation

This strcuture supports operations such as insertion, deletion, updating and traversals.

## Size

Normally programming languages has fixed sizes for this structure, but some languages like Python adjusts their size dynamically as long as elements are added or removed.

## Time complexity

- Accessing an element by index: $O(1)$
- Searching for an element (iterating over it): $O(n)$
- Insertion or deletion at the end of the list: $O(1)$
    ```python
    my_list = [1, 2, 3]
    my_list.append(4) # [1, 2, 3, 4]
    my_list.pop() # [1, 2, 3]
    ```
- Insertion or deletion at a specific index: $O(n)$
    ```python
    my_list = [1, 2, 3]
    my_list.insert(0, 0) # [0, 1, 2, 3]
    my_list.pop(2) # [0, 1, 3]
    ```
- Appending one list to another: $O(k) | K = len(2° list)$
    - Applies for concatenation with +
    - Applies for concatenation with `.extend()`

- Slicing a list: $O(k) | K = len(sublist)$


