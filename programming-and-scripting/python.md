# Python

## Libraries

* Requests ([Documentaton](https://docs.python-requests.org/en/latest/)).
* OS PATH ([Doc](https://www.geeksforgeeks.org/os-path-module-python/))

```
os.system('java -jar ysoserial.jar %s "%s" > %s.txt' % (payload, cmd, payload))
payload_file = open('./' + payload + '.txt', 'rb')
```

## BeautifulSoup&#x20;

Link [tutorial](https://www.dataquest.io/blog/web-scraping-python-using-beautiful-soup/). Web Scraping with Python Using Beautiful Soup

## Functions

### Startwith()

The `startswith()` method returns True if the string starts with the specified value, otherwise False.

_string_.startswith`(_value, start, end_)`

_value_ : Required. The value to check if the string starts with

_start_ : Optional. An Integer specifying at which position to start the search

_end_ : Optional. An Integer specifying at which position to end the search

### Split()

the `split()` method splits a string into a list. You can specify the separator, default separator is any whitespace.

> **Note:** When maxsplit is specified, the list will contain the specified number of elements _plus one_.

_string_.split(_separator, maxsplit_)\[0,1,2] etc to specify which item to show

_separator_ : Optional. Specifies the separator to use when splitting the string. By default any whitespace is a separator

_maxsplit_ : Optional. Specifies how many splits to do. Default value is -1, which is "all occurrences".

### Join()

The `join()` method takes all items in an iterable and joins them into one string. A string must be specified as the separator.



```python
myTuple = ("John", "Peter", "Vicky")  
  
x = "#".join(myTuple)  
  
print(x)
## John#Peter etc
```

### Rstrip()

The rstrip() method **removes trailing spaces or characters from the right side of a string**. The program will remove all white space characters by default if you do not specify a character to remove.

```
variable.rstrip()
```



