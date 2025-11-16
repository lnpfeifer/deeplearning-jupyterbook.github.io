# 0. Environment Setup

To run deep learning code on your local computer, one needs to install different libraries. In this 
tutorial, we will see how to set up a deep learning environment.

## Operating systems

In order to run the code on GPU, install the latest CUDA Driver for your native operating system.

### Windows

If you're a Windows user, install 
[The Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).

    wsl --install

Follow the instructions and reboot your system.

After that, you simply open the WSL terminal (the penguin icon).
The first time you have to update all packages:
    
    sudo apt update && sudo apt upgrade

Python is already installed in WSL.

```{admonition} libgl error
:class: error

To use some of the computer vision libraries in WSL you need to install `libgl`:

    sudo apt install --yes libgl1-mesa-dev
```
    

```{admonition} CUDA error
:class: error

If your notebooks crash when calling the `cuda()` function and get this error: 
`Could not load library libcudnn_cnn_infer.so.8.` The solution is to add the library to 
[*.bashrc file*](https://discuss.pytorch.org/t/libcudnn-cnn-infer-so-8-library-can-not-found/164661).

Go to your file browser, navigate to `Linux/Ubuntu/home/<user_name>`, open the `.bashrc`file and add
this line to the end of the file:

    export LD_LIBRARY_PATH=/usr/lib/wsl/lib:$LD_LIBRARY_PATH

Restart all Ubuntu terminals and the issue should be resolved.
```

### Linux and macOS

There are no extra preparations you need to do.

***

## Virtual environment

A virtual environment is a modular solution to install an independent set of packages for 
different purposes. A "virtual environment" is essentially a single folder that does not affect 
the whole system and can easily be deleted.


To install a virtual environment with `pip`, you should follow 
[the official installation guide](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/).

Pip is a package-management system written in Python and is used to install and manage software 
packages. To install on your system:

    sudo apt install python3-pip

Next, we install the virtual environment:

    python3 -m pip install --user venv

### Creation

To create a virtual environment, you use the command `python3 -m venv <path_dir>` where <path_dir>
is the directory to install the virtual environment. For instance to create a virtual environment
with the name "mbb" in the home directory:

    python3 -m venv ~/mbb

### Activation

To access this environment, you should activate it in the terminal:

    source ~/mbb/bin/activate

If activated successfully, you see on the left side of your terminal the name `(mbb)`.

```{admonition} Important Note
:class: important
You must always remember to activate the virtual 
environment, for example, before installing any package with pip. Otherwise, it's installing it in 
another environment.
``` 

Keep in mind that you can activate the same environment in multiple terminals. This is handy
for installing packages in one terminal and using the environment in another terminal.

A virtual environment can be deactivated by command:

    deactivate

### Installing packages
When you install packages inside a virtual environment, they are isolated from your system-wide
Python installation. It means you can install specific versions of libraries for this project 
without affecting other projects.

Installing packages with pip is very easy. For instance, to install `jupyterlab`:

    pip install jupyterlab notebook

To run the tutorial codes, we will use the PyTorch framework that can be installed:

    pip install torch torchvision torchaudio

```{admonition} ImportError: No module named X
:class: error
Importantly, if you get an `ImportError: No module named X` in a Python script. The solution is
often easy and correct pip installation commands can be found by googling.

For instance `ImportError: No module named cv2` can be resolved by installing `opencv-python`:

    pip install opencv-python 
```
### Using Jupyter Notebook in WSL on Windows
When Running Jupyter Notebook inside WSL, it is slighlty different from running it directly on Windows
When you start Jupyter, it runs in the Linux environment, so it cannot automatically open your 
Windows browser.
A recommended workflow after installing all necessary packages and WSL is as following:
1. Open your WSL terminal and activate your virtual environment:
```
source ~/mbb/bin/activate
```
2. Start Jupyter Notebook (or JupyterLab)
```
jupyter notebook
```
3. In the terminal, you will see a URL that looks like:
```
http:/localhost:8888/
```
Copy it into a browser.
