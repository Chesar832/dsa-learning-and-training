# Static Arrays

## What's an array?
An array is a type of data structure which store elements that can be accessed via indexing. For the case of Python, it uses zero-based indexing which given an array of $n$ elements indexes begins with 0 until the $n-1$ and it supports negative indexing from the -1 for the last element, until the -n index as well.

## What's a static array?
There's two types of arrays, statically sized arrays and dynamically sized arrays:

1. Statically sized arrays: An array with a static number of elements since the creation of the structure.
2. Dynamically sized arrays: An array that can change its number of elements throughout the program or algorithm we design.

Not all programming languages has both type of arrays as built-in fearures and most of them can be intialized in compile time, but if the programming language that you're using allows to skip this step, the initial values of the array will depend on the specific programming language that we're using.

## Characteristics
Arrays are allocated in memory as an interrumped block of memory with sequential locations for its elements which is both memory and time efficient.

A **static array is efficient because it is a fixed-sized and homogeneous structure** whichs allows the computer determine the exact required memory as well as separate that memory in the system as sequential slots without the need to move them after.

- **Fixed-size structures:** Static arrays have a fixed size, meaning their length is determined at the time of creation and cannot be changed later. This characteristic ensures predictable memory usage and simplifies memory management, but it also requires careful planning to allocate the correct size upfront.

- **Homogeneous structures:** Many programming languages handle arrays as homogeneous structures (this is very helpful for the system because it's easier to compute the required space in memory), meaning they must contain elements of the same type. However, Python uses heterogeneous arrays, allowing them to contain elements of different types.

## At a low level, how do arrays work in Python?

In Python, arrays are implemented as lists, which are dynamic and heterogeneous by nature. Unlike static arrays in other programming languages, Python lists can grow or shrink in size and can store elements of different data types.

However, Python also provides the `array` module for creating arrays that are more memory-efficient and type-restricted, but it's still a dynamic structure.

Let's use a simple example to explain how python arrays works:

```python
# Array with an int, string and dictionary
example = [1, "hi", {"key1":10, "key2":20, "key3":30}]
```

Considering the nature of Python arrays, how it can assign memory if each element have a different type and weight? and how does Python do to make it dynamic?.

Well, first let's see **how Python makes possible heteregenuous arrays**.

### Heterogeneous Nature

Turns out that Python indeed is storing the same type of objects in the array `example`. Wait, what? Yeah, at a low level Python doesn't treat directly the actaul value of the defined objects, instead it uses references to those objects (`pointers`) behind the scenes, so our example actually is seen like this by Python:

```python
# Array of pointers
example = [ptr1, ptr2, ptr3]
```

So, Python is using the same type of object in every array (`PyObject`). The work in memory is a little different but a bit intuitive at this point.

Python separates consecutive memory space for all the references (pointers -> `PyObject`) which has the same weight in memory like this:

```python
# Array of pointers (PyObjects)
example = [ptr1, ptr2, ptr3]

# In memory (consecutive memory slots)
# example -> 0x1001 0x1002 0x1003
```

The flexibility comes with this references (pointers) because they carry information about our objects:

1. Type: type of the object like `int`, `dict`, `tuple`, etc.
2. Value: the actual value of our objects like `1`, `{"a":15}`, `(15, 20)`, etc.
3. Reference count: counts how many objects are being refered to the current object. 

> The reference count is very useful for python to liberate memory of objects that has zero references (the were eliminated), as a rule of thumb each object we create has at least 1 as reference count because at the intialization it has one reference from it to itself.

Even though as pointers they share a continous space in memory in addition to a shared type of object, they are just references because the actual object is stored in other space in non-contigous memory slots. Just like this:

```python
# Array of pointers (PyObjects)
example = [ptr1, ptr2, ptr3]

# Pointers in memory (consecutive memory slots)
# example -> 0x1001 0x1002 0x1003

# Refered objects by pointers in memory (non-consecutive memory slots)
# example -> 0x7fae001  0x7bae123  0x7fae03ff
```

This feature makes Python flexible in contrast of languages like C++, but less efficient in memory and speed management, because it has to pass more info in exchange of that flexiblity.

### Dynamic Nature

Now that we already knew how is possible to handke different types of objects by python (heterogeneous feature), let's see how it does them flexible in terms of size.

Even tough Python uses the same object (pointers) to handle a shared type of object for its arrays likewise the structure holds the weight of all elements stored in it. So, to handle dynamically this structure, python has certain rules written in its base in C (`CPython`) which evaluates the total weight of the array and reserves more memory to handle more insertions.

```python
# Array of pointers (PyObjects)
example = [ptr1, ptr2, ptr3]

# How actually it is in memory
# example = [0x1001 0x1002 0x1003 reserved reserved]
```

It's important to know that the reserved space is changing in terms of size of bits or chunks of elements and by predefined rules, so it won't be increasing with the same step of bytes size everytime. This extra space is computed based on the current weight in bytes of the array.

Next there's an example to see this happening:

```python
import sys

lst = []
for i in range(20):
    lst.append(i)
    print(f"Length: {len(lst):2}, Size in bytes: {sys.getsizeof(lst)}")

# Output
# As we append elements to the list, observe how the size in bytes changes:
# Initially, the list has no elements and occupies 56 bytes.
Length:  0, Size: 56

# Adding the first element increases the size to 88 bytes.
Length:  1, Size: 88

# Adding more elements (up to 4) does not increase the size further.
Length:  2, Size: 88
Length:  3, Size: 88
Length:  4, Size: 88

# Adding the fifth element triggers an increase in size to 120 bytes.
Length:  5, Size: 120

# The size remains 120 bytes for the next few elements.
Length:  6, Size: 120

# Adding the ninth element increases the size to 184 bytes.
Length:  9, Size: 184
Length: 10, Size: 184

# Adding the fourteenth element increases the size to 256 bytes.
Length: 14, Size: 256
Length: 15, Size: 256

# Adding the sixteenth element increases the size to 328 bytes.
Length: 16, Size: 328
```

Again, this feature makes Python more flexible, but less efficient because it's using extra space for arrays that can be unused if we already know how many elements are we going to have.
