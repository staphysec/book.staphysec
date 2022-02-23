# Virtualenv & Switching Versions

If you are having issue using tools that require diferent python version then this i for you :smile:

## Automate the Conversion from Python2 to Python3

Taken from [geekforgeeks](https://www.geeksforgeeks.org/automate-the-conversion-from-python2-to-python3/).



**Installation**

This module does not come built-in with Python. To install this type the below command in the terminal.

```
pip install 2to3
```

**Syntax:**

```
2to3 [file or folder] -w
```

If we want to change all files in the currently open folder and all the files in the subfolder from Python2 to Python3 type the below command.

```
2to3.-w
```

If we want to change a particular file in the current folder from Python2 to Python3 then enter the following command.

```
2to3 gfg.py -w
```

## Virtualenv

