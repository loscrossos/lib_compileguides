
# opencv-python

Compilation of opencv-python is straight forward. 

**update 2025.10:**
currently you only need to pre-merge a PR that enables pyton 3.13+ compatibility. here on windows for python 3.13
see: https://github.com/opencv/opencv-python/pull/1142
Example on windows.


### Linux pre-requisites:
if you havent already you should install the dev headers
```
sudo apt-get install python3-dev python3-numpy
```

### get the code
we clone the repository and update the linked repos to the latest version (as some bugfixes are only in the latest version of opencv: such as ffmpeg bug see https://github.com/opencv/opencv/issues/27907 )
```
git clone --recursive https://github.com/opencv/opencv-python.git && cd opencv-python && git submodule update --init --recursive --remote
cd  opencv-python
```

we need the updated opencv but the build process will reset it. to prevent that we fake commit the repos (we will not push them). this is only for the build process.

```
git add opencv opencv_contrib && git commit -m "update submodules to latest"
```
**optional as of 2025.10**
open-cv is currently broken on pipy for Python 3.13 or 3.14. you need to merge a PR for it to work .
```
git remote add upstream https://github.com/opencv/opencv-python && git fetch upstream && git fetch upstream pull/1142/head:pr-1142 && git merge pr-1142 
```


### create venv
Windows
```
py -3.13 -m venv .envwin 
.envwin\Scripts\activate
```

Linux
```
python3.13 -m venv .envwin 
. ./.envwin/bin/activate
```

```
python -m pip install --upgrade pip
pip install wheel setuptools  scikit-build cmake numpy
```
### compile

**(Optional on Linux)**: GCC compatibility

Pytorch was built with gcc11. Current version on Ubuntu24.04LTS is gcc13. Wheels built with it will not run on Linux systems with older versions (e.g. Ubuntu 22.04LTS). To maximize compatibility we can build with gcc11. We need to install it first.

```bash
sudo apt install g++-11 gcc-11
```
now we  can set it to be used for compilation:
```bash
export CXX=g++-11 && export CC=gcc-11
```


**CrossOS**

```
#optional for headless lib
# windows
set ENABLE_HEADLESS=1
#linux
export ENABLE_HEADLESS=1


pip wheel . --verbose
pip wheel . --verbose --no-build-isolation 


```

a wheel appears in a directory shown during the compile process



