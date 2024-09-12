# structure, setup

1. Fork the Repository
    1. https://github.com/codio-content/pixel_art
    2. clone from own github repo
        1. `https://github.com/lennon-c/pixel_art.git`
    3. populate project


```bash
git clone git@github.com:lennon-c/pixel_art.git
git clone https://github.com/lennon-c/ScanPyImports.git
```


```
pixel_art/
├── .git
├── README.md
├── setup.py
├── pixel_art/
│   ├── __init__.py
│   ├── examples.py
│   ├── pixels.py
│   └── pa-env/ # everinment package 
└── tests/
```

```bash
cd labs\pixel_art\pixel_art
py -m venv pa-env
pa-env\Scripts\activate 
py -m pip install --upgrade pip setuptools wheel pipenv
py -m pip install colorama
```


# coding 
## Import statements 

### __init__.py
```python
# __init__.py
import pixel_art.examples, pixel_art.pixels
```

### scripts 
```python
# import pixel_art.pixels as pixels
import pixels
```

to import the module `pixels`
- in **development** we import pixels as `import pixels`, based on cwd
- for **deployment**  `import pixel_art.pixels as pixels`, otherwise it will not work! 

# Creating a Wheel

create a `setup.py` file. 
- `pixel_art` depends on the `coloroma` package. 

```python
# setup.py
from setuptools import setup

setup(
   name='pixel_art',
   version='0.1',
   description='Package for drawing pixel art to the terminal.',
   author='Carolina Lennon',
   packages=['pixel_art'], 
   install_requires = ['colorama']
)
```

this is the recommendation from python org 
- run outside of the env
```bash
cd pixel_art 
py -m build
cd dist
dir /A /B
# pixel_art-0.1-py3-none-any.whl
# pixel_art-0.1.tar.gz
```


this is in the lab
```bash
cd pixel_art
python3 setup.py sdist bdist_wheel
```

# Testing the Package

create a env

```bash
py -m venv smile
smile\Scripts\activate 
py -m pip install "D:\Dropbox\Python\Courses\Packaging in Python\labs\pixel_art\dist\pixel_art-0.1-py3-none-any.whl"
```

```bash
py -m pip freeze
# colorama==0.4.6
# pixel_art @ file:///D:/Dropbox/Python/Courses/Packaging%20in%20Python/labs/pixel_art/dist/pixel_art-0.1-py3-none-any.whl

pip list
"""
Package    Version
---------- -------
colorama   0.4.6
pip        22.3.1
pixel_art  0.1
setuptools 65.5.0
"""
```