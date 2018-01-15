# Python Programming

## Data Types

### Dictionaries

#### Validity

These are data types that store data in form of key-value pairs. The only thing worth noting here is that **keys** need to be immutable variables, i.e. they cannot be lists of other dictionaries because they are mutable by their very definition.

#### Check for existence

In order to quickly check whether or not a key exists in a particular dictionary, use the syntax `"key" in dict`  which would return `True` if the key is present in the dictionary object `dict`.

#### Deletion

The obvious function for most deletions, `del` is used for **deleting** a **key-value pair** in any dictionary with the syntax being `del(dict["key"])`.