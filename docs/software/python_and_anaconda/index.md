# Python and Anaconda

## Python Modules
### Overview 
Different versions of Python are available on HPC both as system modules as well as system software on each compute node. Python 2 is available but is no longer supported by the Python Foundation, so we recommend you use Python 3. Python version 3 requires the python3 command or pip3 list to differentiate.  It is very different from Python version 2, so do not assume that Python 3 will work for you or that all older modules will work with version 3.

### Installation and Package Policy

We maintain a two tiered approach to Python packages

* Tier 1: We install the basic Python packages that are required by most users (these are mostly libraries rather than packages, such as numpy and scipy). This is done for the versions of Python that we install as modules. Adding some packages might force an upgrade of numpy for example, which might break a user's environment that was dependent on the prior version.

* Tier 2: For packages that we do not provide we STRONGLY recommend the use of virtualenv, which is detailed below and provides a custom and easy to use person Python environment.

### Available Python Versions

!!! danger "Python 2 is no longer officially supported by the Python Software Foundation."

Six versions of Python are available on HPC. They are only available on compute nodes and are accessible either using a batch submission or interactive session. 

|Version|Accessibility[^1]|
|-|-|
|Python 2.7.5|system version (no module)|
|Python 3.6.8|system version (no module)|
|Python 3.6.5|module load python/3.6/3.6.5|
|Python 3.8.2|module load python/3.8/3.8.2|
|Python 3.9.10|module load python/3.9/3.9.10|
|Python 3.11.4|module load python/3.11/3.11.4|

### Installing Python Packages Using a Virtual Environment

???+ tip "Virtual environment tips"
    * Useful overview of virtualenv and venv: [InfoWorld Article: Python virtualenv and venv do's and don'ts](https://www.infoworld.com/article/3306656/python/python-virtualenv-and-venv-dos-and-donts.html?idg_eid=33b8cb1248bcd5c9ddcec9cbccd1b5cb&email_SHA1_lc=579ec7d94c8828baab0995f0b5d55ab21c1a5f2a&cid=ifw_nlt_infoworld_daily_2018-09-19&utm_source=Sailthru&utm_medium=email&utm_campaign=InfoWorld%20Daily:%20Weekday%20Edition%202018-09-19&utm_term=infoworld_daily)
    * In the following instructions any module commands have to be run from an interactive session on a compute node
<div style="float: right; width: 0px; height: 1px"></div>
<div style="float: right; clear: right"><iframe width="420" height="315" src="https://www.youtube.com/embed/YOSkjsTVtrc" allowfullscreen></iframe></div>

One of the best things about Python is the number of packages provided by the user community. On a personal machine, the most popular method today for managing these packages is the use of a package manager, like ``pip```. Unfortunately, these may require root access preventing you from being able to successfully install the libraries you need.

There is an easy solution, however. You can use a virtual environment to create a personal python environment that will persist each time you log in. There is no risk of packages being updated under you for another user and allows greater control over your environment.

Virtual Environment Instructions

1. Set up your virtual environment in your account. This step is done one time only and will be good for all future uses of your Python environment. You will need to be in an interactive session to follow along. 
 
    Note: In the commands below, ```/path/to/virtual/env``` is the path to the directory where all of your environment's executables and packages will be saved. For example, if you use the path ```~/mypyenv```, this will create a directory in your home called ```mypyenv```. Inside will be directories ```bin```, ```lib```, ```lib64```, and ```include```. 

    === "Python Version $\geq$ 3.8"
        ```bash
        module load python/<version>
        virtualenv --system-site-packages /path/to/virtual/env
        ```
    === "Python Version $<$ 3.8"
        ```bash
        module load python/<version>
        python3 -m venv --system-site-packages /path/to/virtual/env
        ```
        
2. To use your new environment, you'll need to activate it. Inside your virtual environment, there's a directory called bin that has a file called activate. Sourcing this will add all of the paths needed to your working environment. To activate, run the following, replacing /path/to/virtual/env with the path specific to your account:

    ```bash
    source /path/to/virtual/env/bin/activate
    ```
3. Once your environment is active, you can use pip to install your python packages.  You should first upgrade to the latest version of pip. For example, to add the pycurl package to the virtual environment:
    
    ```bash
    pip install --upgrade pip
    pip install pycurl
    ```
4. That's it! As long as your virtual environment is active, you will have access to the packages installed there. Virtual environments deactivate when you log out, so for each subsequent session or in batch jobs, you will just need to reactivate the environment to get access to your packages:
    ```bash
    module load python/<version>
    source /path/to/virtual/env/bin/activate
    ```

### Custom Jupyter Kernel

!!! warning 
    The default version of Python available in an OnDemand Jupyter Notebook is 3.8.2. If you would like to create a virtual environment using a standard Python module, you will need to use Python version 3.8.2. If you want to use a different version of python, you can use an Anaconda environment.

If you want to make one of your virtual environments available for use in one of our Open OnDemand Jupyter Notebooks, you can do so by creating a custom kernel. To do this, start an interactive terminal session and activate your environment (if you do not have an environment, refer to the sections above on how to do so):

```bash
module load python/3.8/3.8.2                     
source /path/to/your/virtual/environment/bin/activate
```

Once your environment is ready to go, pip-install ```jupyter``` and create your own custom kernel. The ```--force-reinstall``` flag will allow you to install the ```jupyter``` package in your local environment and will not affect the system version. This will create a directory in ```~/.local/share/jupyter/kernels/``` in your account. In the following commands, replace ```<your_environment>``` with the name of your own environment: 

```bash
pip install jupyter --force-reinstall
ipython kernel install --name <your_environment> --user 
```

Once you've successfully created your kernel, go to [Open OnDemand](https://ood.hpc.arizona.edu/) and start a Jupyter Notebook. Once the session starts, open it and click the "new" dropdown menu in the upper right. If everything is working correctly, you should see your custom kernel's name. For example, if the custom kernel's name was ```py38-env```:

<img width="300" src="images/use-py38-custom-kernel.png">

Once you've selected your environment, try loading a custom package you've installed to check that everything is working as expected. In this example, we'll check with the non-standard package ```emoji``` which has been installed in this environment:

<img width="800" src="images/py-38-test.png">

## Anaconda

### Overview

We have three versions of Anaconda installed as system modules for use. You can initialize these in your home directory for access and package management. 

|Version|Accessibility|
|-|-|
|2020.02|```module load anaconda/2020.02```|
|2020.11|```module load anaconda/2020.11```|
|2022.05|```module load anaconda/2022.05```|

### Initializing Anaconda

Initializing Anaconda in your account only needs to be performed once and is what makes Anaconda available and ready for customization (e.g., installing custom packages) in your account. 

!!! tip 
    * Conda will direct you to close and reopen your shell to complete the initialization process. You can skip this by running the command ```source ~/.bashrc``` listed in the instructions below. 
    * Running ```conda config --set auto_activate_base false``` is highly recommended. Conda contains a lot of accompanying software which may interfere with other software. 
    
In an interactive session:

```bash
module load anaconda/<version>
conda init bash                  
source ~/.bashrc  
conda config --set auto_activate_base false
```

### Creating a Conda Environment
Once conda has been configured following the steps above, you can create a local environment. This allows you to control the version of Python you want to use, install your own software, and even create custom Juypyter kernels (making your environment accessible in an OnDemand notebook). To do this, you can use the command ```conda create```. For example, in an interactive session:

```bash
conda activate
conda create --name py37 python=3.7 # Build a local environment with a specific version of python
conda activate py37
```

To view the environments available to you, use the command

```bash
conda env list
```

### Installing Conda Packages and Other Software

Once you have created a conda environment, you can install the packages you need. To do this, follow the software-specific installation instructions. This may be as simple as running "conda install <my_package>", or it may involve installing a handful of dependencies. If the installation instructions ask you to create a new environment, you do not have to repeat this step. 

Once you have performed the install, you should then be able to access your software within this environment. If you are unable to load your software, check your active environment with

```bash
conda info
```

and the installed packages with 

```bash
conda list
```

### Custom Jupyter Kernel

If you want to make one of your conda environments available for use in one of our Open OnDemand Jupyter Notebooks, you can do so by creating a custom kernel. To do this, start an interactive terminal session and activate your environment:

```bash
conda activate
conda activate <your_environment>
```

Next, pip-install Jupyter and use it to create a custom kernel using the command ```ipython``` and replacing ```<your_environment>``` with your own environment's name:

```bash
pip install jupyter
ipython kernel install --name <your_environment> --user
```

Once you've configured your kernel, go to [Open OnDemand](https://ood.hpc.arizona.edu/) and start a Jupyter notebook. Once the session starts, open it and click the "new" dropdown menu in the upper right. If everything is working correctly, you should see your custom name. For example, if you created a conda environment with the kernel name py38, you should see the following:

<img width="300" src="images/conda-custom-kernel.png">

Once you've selected your environment, try checking the Python version in your notebook using the ```sys``` module. Additionally, for demonstration purposes, we'll check that a custom package installed in py38 (emoji) can be imported and is working. 

<img width="800" src="images/conda-kernel-testing.png">


[^1]: Note: The command ```python``` defaults to the system 2.7.5 version. To use Python 3, use the command ```python3```.