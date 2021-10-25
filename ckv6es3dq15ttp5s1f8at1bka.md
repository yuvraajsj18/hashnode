## How to Use Python Dictionaries

# Introduction

In this article, we will cover different ways of defining a dictionary, how to access and update values of a dictionary, the dictionary’s built-in methods, and how to use dict comprehension. 

We will also learn about restrictions on keys of a dictionary, membership operators, pretty-printing a dictionary, and making a shallow copy vs deep copy of a dictionary. 


# What is a dictionary in Python?

Python provides several useful data types built-in, Dictionary is one such data structure.

*A dictionary is a collection of key: value pairs where each value is accessed using a unique key.*

This is in contrast to the *list* where elements are accessed using their indexes.

We can think of a dictionary as a table with two columns:

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635149690035/ReQ8RT05H.png)

> Highlights:
- A dictionary is a collection of key: value pairs where each value is accessed using a unique key.

# How to define a dictionary?

We can define a dictionary in three different ways. Let's see each one of them by converting the above pictorial representation of the dictionary into a real python one.

### Using curly braces `{}`

We can use the curly braces to define a dictionary by providing key-value pairs separated by a '**:'** as `key: value`:

```python
harry_info = {
    "name": "Harry",
    "age": 11,
    "house": "Gryffindor",
}

print(harry_info)
print(type(harry_info))  # <class 'dict'>
```

Notice that a dictionary can have values of different types.

We can also create an empty dictionary using `{}` as: `empty_dict = {}`.

### Using `dict()` function

We can create a dictionary by passing a list of tuples to the *dict* function:

```python
harry_info = dict([
                   ("name", "Harry"),
                   ("age", 11),
                   ("house", "Gryffindor")
])

print(harry_info)
```

### Using keyword arguments in `dict()`

We can provide keyword arguments to the *dict* function when all keys are *string*:

```python
harry_info = dict(
    name = "Harry",
    age = 11,
    house = "Gryffindor"
)

print(harry_info)
```

## Values in a dictionary

A dictionary can store any type of value including another dictionary. Let's change the *harry_info* dictionary to contain a nested dictionary *house* and a list of *friends:*

```python
harry_info = {
    "name": "Harry",
    "age": 11,
    **"house": {
      "name": "Gryffindor",
      "Animal": "Lion",
      "Element": "Fire"   
    },
    "friends": ["Ron", "Hermione"]**
}

print(harry_info)
```

**Tip** 💡

When we print the above dictionary the output would not be very readable, we can use the `pprint` function to pretty print a dictionary:

```python
from pprint import pprint

pprint(harry_info)
```

Output:

```python
{'age': 11,
 'friends': ['Ron', 'Hermione'],
 'house': {'Animal': 'Lion', 'Element': 'Fire', 'name': 'Gryffindor'},
 'name': 'Harry'}
```

## Restrictions on keys

There are two restrictions we need to know when defining keys:

1. **Duplicate keys are not allowed**
    
    If we define the same key twice, the second occurrence will override the first one:
    
    ```python
    duplicate_dict = {
        "first": 0,
        "second": 2,
        "first":1
    }
    
    print(duplicate_dict)
    ```
    
    This will print:
    
     `{'first': 1, 'second': 2}` ✅
    
    and not
    
    `{'first': 0, 'second': 2}` ❌
    
    `{'first': 0, 'second': 2, 'first': 1}` ❌
    
2. **Keys must be immutable**
    
    Keys must have a type that is immutable, which means any type whose value doesn't change once created like *int, bool, str, float, etc.*
    
    That's why we can have a *tuple* as a key but not a *list:*
    
    ```python
    example_dict = {
        (1, 2): "Tuple",  # Okay to use
        False: "Bool",    # Okay to use
        1: "int",         # Okay to use
        [1, 2]: "list",   # raises TypeError
    }
    ```
    
    Using a list as a key raises *TypeError: unhashable type: 'list'* because it is a mutable object. 
    
    Technically, a key requires a *hashable* value which means that Python's built-in hash() function should return a *unique hash value* for that object and all immutable types satisfy this condition.
    
> Highlights:
- We can define a dictionary using:
    - Key-value pairs in curly braces.
    - Using dict function
- A dictionary can have any type of value.
- Key cannot be:
   - Duplicated
   - Mutable (more precisely unhashable)


# How to access values in a dictionary?

We can access a value from a dictionary by using the square brackets `[]`.

 So `dict_name[key]` will return the corresponding *value.*

Let's try to retrieve some values from the *harry_info* dictionary:

`print(harry_info["name"])`

Output: "Harry"

`print(harry_info["friends"])`

Output: ['Ron', 'Hermione']

**What if we try to retrieve a value using a key that doesn't exist?**

Let's try that too:

`print(harry_info["enemies"])`

Output: KeyError: 'enemies'

We got a key error which means that *we can not retrieve keys that don't exist using the square bracket syntax.*

### Adding a new key-value pair to the dictionary

As *dictionaries are mutable structures*, we can add new members by assigning values to new keys using the same square bracket operator:

Syntax: `dict_name[new_key] = value`

```python
harry_info["enemies"] = ["Voldemort", "Death Eaters"]
```

### Updating existing key-value pair of a dictionary

We can also update the key's values similarly using the square brackets:

Syntax: `dict_name[key] = new_value`

```python
harry_info["age"] = 17
```

This will update the *age* key from 11 to 17.

### Using Membership operator with dictionaries

We can use the `in` and `not in` operators to check whether a key exists in the dictionary or not:

```python
print('name' in harry_info)     # Output: True

print('name' not in harry_info) # Output: False

print('year' in harry_info)     # Output: False

print('year' not in harry_info) # Output: True
```

### Get the number of key-value pairs

Use the built-in *len* function to get the number of key-value pairs in a dictionary:

```python
print(len(harry_info))  # Output: 5
```

> Highlights:
- Access values using dict_name[key] syntax.
- Add a new value using dict_name[new_key] = value.
- Update a value using the same syntax as (2).
- Use in and not in operator to check for key existence in a dictionary.
- Use the len function to get the number of key-value pairs.

# Built-in Dictionary Methods

### get(key, default=None)

This is an alternative to the `[]` for accessing the values using a key from a dictionary. The difference is that we can provide a default value to return when a key doesn't exist instead of raising a key error.

```python
print(harry_info.get("name"))     # Output: Harry
print(harry_info.get("year"))     # Output: None
print(harry_info.get("year", 7))  # Output: 7
```

### items()

Returns a list of tuples containing the key-value pairs of a dictionary.

```python
print(list(harry_info.items()))
```

Output:

```python
[('name', 'Harry'), ('age', 17), ('house', {'name': 'Gryffindor', 'Animal': 'Lion', 'Element': 'Fire'}), ('friends', ['Ron', 'Hermione']), ('enemies', ['Voldemort', 'Death Eaters'])]
```

We can use the *items* method to loop through a dictionary:

```python
for key, value in harry_info.items():
  print(key, 'is', value)
```

Output:

```python
name is Harry
age is 17
house is {'name': 'Gryffindor', 'Animal': 'Lion', 'Element': 'Fire'}
friends is ['Ron', 'Hermione']
enemies is ['Voldemort', 'Death Eaters']
```

### keys()

Returns the list of all keys of a dictionary.

```python
print(list(harry_info.keys()))
```

Output: `['name', 'age', 'house', 'friends', 'enemies']`

### values()

Returns the list of all values of a dictionary.

```python
print(list(harry_info.values()))
```

Output: `['Harry', 17, {'name': 'Gryffindor', 'Animal': 'Lion', 'Element': 'Fire'}, ['Ron', 'Hermione'], ['Voldemort', 'Death Eaters']]`

### pop(key[, default])

Remove the specified key and return the corresponding value.

If the key is not found, d is returned if given, otherwise KeyError is raised.

```python
print(harry_info.pop('enemies'))    # enemies will be removed
print(harry_info.pop('invalid_key', "Invalid Key"))
print(harry_info.pop('invalid_key'))
```

Output:

```python
['Voldemort', 'Death Eaters']
Invalid Key
KeyError: 'invalid_key'
```

### popitem()

Remove and return the last (key, value) pair as a tuple, but raise KeyError if dictionary is empty.

```python
print(harry_info.popitem())
```

Output: `('friends', ['Ron', 'Hermione'])`

### update(iterable)

Merges a dictionary with another dictionary or with an iterable of key-value pairs.

If the dictionary or iterable passed has the same key as the original dictionary then the value of that key is overridden.

**When iterable is a dictionary**

```python
d1 = {'a': 1, 'b': 2, 'c': 3}
d2 = {'b': 200, 'd': 4}

d1.update(d2)

print(d1)
```

Output: `{'a': 1, 'b': 200, 'c': 3, 'd': 4}`

Notice how 'b' is updated and 'd' is added.

**When iterable is a list of tuples**

```python
d1 = {'a': 1, 'b': 2, 'c': 3}

d1.update([('b', 200), ('d', 4)])

print(d1)
```

Output: `{'a': 1, 'b': 200, 'c': 3, 'd': 4}`

We can also provide a keyword arguments to update and the result will be the same:

```python
d1 = {'a': 1, 'b': 2, 'c': 3}

d1.update(b=200, d=4)

print(d1)
```

Output: `{'a': 1, 'b': 200, 'c': 3, 'd': 4}`

### fromkeys(iterable, value=None)

Create a new dictionary with keys from iterable and all values set to value.

```python
keys = ("key1", "key2", "key3")
example_dict = dict.fromkeys(keys, "default value")
print(example_dict)
```

Output: `{'key1': 'default value', 'key2': 'default value', 'key3': 'default value'}`

### setdefault(key, default=None)

Return the value for key if key is in the dictionary, otherwise insert that key with a value of default and return default.

```python
# Returns value for 'name'
print(harry_info.setdefault("name"))   
# Returns value for 'name', default is ignored
print(harry_info.setdefault("name", "Harry Potter"))
# Adds key 'last_name' and return its value 'Potter'
print(harry_info.setdefault("last_name", "Potter"))  
```

 Output:

```python
Harry
Harry
Potter
```

### copy()

Performs a shallow copy of the dictionary.

```python
harry_copy = harry_info.copy()
print(harry_copy)
```

**Shallow copy vs deep copy**

With a shallow copy if the original dictionary contains mutable values they won't be copied, therefore changing the copied dictionary will change the original one.

We can use *copy.deepcopy* method to perform a deepcopy as shown below:

```python
from copy import deepcopy

d = {
    'number': 1,
    'list': [1, 2]
}

d_shallow = d.copy()
d_shallow['list'].append(3)
print("shallow copy", d_shallow)
print("original dict", d)     # d is also changed

d_deep = deepcopy(d)
d_deep['list'].append(4)
print("deep copy", d_deep)
print("original dict", d)    # d is unchanged
```

Output:

```
shallow copy {'number': 1, 'list': [1, 2, 3]}
original dict {'number': 1, 'list': [1, 2, 3]}
deep copy {'number': 1, 'list': [1, 2, 3, 4]}
original dict {'number': 1, 'list': [1, 2, 3]}
```

### clear()

Remove all items from a dictionary

```python
harry_info.clear()
print(harry_info)
```

Output: `{}`

> Highlights:
- Dictionary provides several methods to access, update, remove, and copy key-value pairs.


# Dict Comprehension

You may be familiar with list comprehensions, it is an alternative to for loop and a concise notation to perform some operations for a collection of elements.

You can also write comprehension for a dictionary using the following syntax:

`example_dict = {key:value for key, value in iterable}`

where the iterable is a list of key-value tuples.

```python
d1 = dict((k, v) for k, v in enumerate("Hello", 1))
print(d1)    # {1: 'H', 2: 'e', 3: 'l', 4: 'l', 5: 'o'}
d2 = {k: v for k, v in enumerate("Bye", 1)}
print(d2)    # {1: 'B', 2: 'y', 3: 'e'}
```

**Enumerate** function returns a key: value pair using the iterable passed to it and the start value.

You can learn more about comprehensions in Python in this article: [Comprehension in Python: Explained](https://blog.yuvraj.tech/comprehensions-in-python-explained).

> Highlights:
- Use dict comprehension to perform operations on key-value pairs of a dictionary in a concise way.

# Summary
- Dictionary is a mutable data structure to store key: value pairs.
- Define a dictionary using curly braces or dict function.
- Access or update values of a dictionary using square brackets.
- Dictionary provides built-in methods to add, update, remove, and copy key-value pairs.
- Use dict comprehensions to perform operations on dict in a concise way.

## Thanks for reading.

If you found this article helpful, please like and share! Feedbacks are welcome in the comments.

---

You may also like:
- [The Mutable Default Argument Mess in Python](https://blog.yuvraj.tech/the-mutable-default-argument-mess-in-python)
- [Comprehensions in Python: Explained](https://blog.yuvv.xyz/comprehensions-in-python-explained)
- [How to Save User's Data Persistently in Web Browser Using Local Storage](https://blog.yuvraj.tech/local-storage-in-javascript)
- [Linux Commands Reference With Examples](https://blog.yuvv.xyz/linux-commands-reference-with-examples)

Connect with me on [Twitter](https://twitter.com/yuvraajsj18), [GitHub](https://github.com/yuvraajsj18), and [LinkedIn](https://www.linkedin.com/in/yuvraajsj18/).
