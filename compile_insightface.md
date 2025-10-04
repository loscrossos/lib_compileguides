# Insightface

Compilation of Insightface is straight forward. here on windows for python 3.13

### get the code

```
git clone https://github.com/deepinsight/insightface 

```
### create venv

```
cd insightface 
py -3.13 -m venv .envwin 
.envwin\Scripts\activate
pip install wheel setuptools Cython numpy
```
### compile

```
cd python-package  
python setup.py bdist_wheel
```

a wheel appears in the newly created folder `dist`

