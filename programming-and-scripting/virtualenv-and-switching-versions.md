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

[Blog1](https://docs.python-guide.org/dev/virtualenvs/) env

[Blog2](https://techviewleo.com/install-python-with-virtualenv-on-linux-mint/)

First install python2

```
sudo apt install python2
```

### Basic Usage

1. Create a virtual environment for a project:

```
$ cd project_folder
$ virtualenv venv
```

`virtualenv venv` will create a folder in the current directory which will contain the Python executable files, and a copy of the `pip` library which you can use to install other packages. The name of the virtual environment (in this case, it was `venv`) can be anything; omitting the name will place the files in the current directory instead.

This creates a copy of Python in whichever directory you ran the command in, placing it in a folder named `venv`.

You can also use the Python interpreter of your choice (like `python2.7`).

```
$ virtualenv -p /usr/bin/python2.7 venv
```

or change the interpreter globally with an env variable in `~/.bashrc`:

```
$ export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python2.7
```

1. To begin using the virtual environment, it needs to be activated:

```
$ source venv/bin/activate
```

Install packages using the pip command:

```
pip install requests
```

```
deactivate
```

This puts you back to the system’s default Python interpreter with all its installed libraries.

To delete a virtual environment, just delete its folder. (In this case, it would be **rm -rf venv**.)

###
