---
title: "Sibling Package Import in Python"
date: 2023-10-30T09:03:20-08:00
draft: false
---

## Sibling Package Import in Python
```
.
├── a.py
├── b.py
└── __pycache__
    └── a.cpython-311.pyc

1 directory, 3 files
```
When our directory structure is like this, there is no problem importing something from a to b or vice versa.
We can do like `from a import hello` and it works fine.

But what if the structure is like this .. 
```
.
├── dirA
│   └── a.py
├── dirB
│   └── b.py
└── __pycache__
    └── a.cpython-311.pyc
```

- 1st try :
```python
from dirB.a import hello
hello()
```
- and it gives error 
```error
ModuleNotFoundError: No module named 'dirB'
```

2nd try :
```python
from ..dirA import a
a.hello()
```
- And it gives different type of error ( but seems better than the previous one )
```
    from ..dirA import a
ImportError: attempted relative import with no known parent package
```

## Solution
- create a virtual environment in the project folder.
- create a `setup.py` file with the following content ..
```
from setuptools import setup, find_packages
setup(name='myproject', version='1.0', packages=find_packages())
```
- Do `pip install -e .`
- Now this works fine.
```python
from dirA import a
a.hello()
```

```
.
├── dirA
│   ├── a.py
│   ├── __pycache__
│   │   └── a.cpython-311.pyc
│   └── subdirA
│       ├── a.py
│       └── __pycache__
│           └── a.cpython-311.pyc
├── dirB
│   └── b.py
├── myproject.egg-info
│   ├── dependency_links.txt
│   ├── PKG-INFO
│   ├── SOURCES.txt
│   └── top_level.txt
├── __pycache__
│   └── a.cpython-311.pyc
├── setup.py
```
- The directory structure is like this and now we can import `dirA/subdirA/a` also. ex:
```python
# dirB/b.py
from dirA.subdirA import a
a.hello2()
# output : Hello world
```

Reference : [stackoverflow](https://stackoverflow.com/questions/6323860/sibling-package-imports/50193944#50193944)