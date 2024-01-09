# R

R is a popular language for data analysis and visualization. Different versions are available as software modules and we provide the graphical interface RStudio for R through our Open OnDemand web interface.

Similar to other languages that use package managers to install libraries contributed by the user community, we recommend you create and manage your own local libraries in your account. This ensures a stable global environment for all users and that you have the most control over your packages' versions and dependencies.

We provide instructions below for how to create, use, and switch between libraries as well as some debugging techniques for when package installations fail. We also provide some script examples (click the button in the banner at the top of this page) for submitting R scripts as batch jobs.

RStudio is a popular method for running analyses (and for good reason!), but for longer-running jobs (say, many hours or days) or workflows that need more flexibility in their environment (e.g., need access to software installed as system modules such as gdal), we recommend batch submissions.

## Creating a Custom Library

!!! tip ""
     R packages can be finicky. See **Switching Between Custom Libraries** and **Common Problems** below to help with frequent user issues.

**Creating your first library**

1. Make a local directory to store your packages
   ```bash
   mkdir -p ~/R/library_4.2
   ```
  
2. Tell R where the directory is by creating an environment file[^1]
    ```bash
    echo 'R_LIBS=~/R/library_4.2/' >> ~/.Renviron
    ```
    
3. That's it! Now you can install packages and they will be stored in the directory you just created. For example, to install and load the package ```ggplot2```:
    ```bash
    module load R/4.2
    R
    install.packages("ggplot2")
    ```

## Switching Between Custom Libraries

If you're using different versions of R, we recommend you use different libraries. See **Common Problems** below for more information. When creating a library, consider including pertinent information in the name such as R version. For example, if you wanted to switch to using R 4.1, you could create a directory called ```library_4.1``` using:
```bash
mkdir -p ~/R/library_4.1
```
Then, to use your new library, edit your ```~/.Renviron``` file[^1] using a text editor such as ```nano```:
```bash
nano ~/.environ
```
Once your text editor opens, rename the ```R_LIBS``` you previously had in your file. In this case, this value would look like:
```bash
R_LIBS=~/R/library_4.1
```
To exit ```nano```, use ++ctrl+x++ and save at the prompt. Once your file is saved, you're ready to start installing files into your new library. 

## Common Problems and How to Debug Them

Working on a cluster without root privileges can lead to complications. For general information on package installations, see the [r-bloggers documentation](http://www.r-bloggers.com/installing-r-packages/). For information on common installation problems on our clusters, see the section below with with suggested solutions:

=== "Anaconda"
    One common reason R packages won't install is an altered environment. This can frequently be caused by the presence Anaconda (or Miniconda) installed locally or initialized in your account from our system module.
    
    When Anaconda is initialized, your ```.bashrc``` file is edited so that it becomes the first thing in your ```PATH``` variable. This can cause all sorts of mayhem. To get around this, you can either remove anaconda from your ```PATH``` and deactivate your environment, or comment out/delete the initialization in your ```~/.bashrc``` if you want the change to be permanent.
    
=== "A Corrupted Environment"

    If Anaconda is not initialized in your account, there might be other culprits that are corrupting your environment.

    Look for any of the file types listed below on your account. If you find them, try removing them (make a backup if you need them) and try the installation again.

    * Saved R sessions. If this is the case, after starting a session, you will get the message "[Previously saved workspace restored]". Old sessions are saved as a hidden file ```.RData``` in your home directory. 
    * Gnu compilers
    * Windows files

=== "Library Issues"

    Have you set up a custom library? Are you switching between custom libraries? You may want to check that everything is being loaded from the correct location and that there are not multiple or unwanted libraries being used.
    
    Double-check that you have an ```.Renviron``` file. This is a hidden file located in your home directory and should set the path to your custom R library. If you do not have a custom library name set up, R will create one for you saved as something like:
    ```bash
    ~/R/x86_64-pc-linux-gnu-library
    ```
    This directory can lead to unwanted behavior. For example, if you're trying to use a new custom library (such as when switching R version), R will still search x86_64-pc-linux-gnu-library for package dependencies and may cause installs to fail. To fix this, rename these types of folders something unique and descriptive.

    To set up/switch custom libraries, follow the instructions in the Creating a Custom R Library section above.

=== "Mixing R Versions"

    Because HPC is a cluster where multiple versions of R are available, users should take care to avoid mixing and matching. Because packages often depend on one another, libraries using different versions of R can turn into a tangled mess.  Common errors that can crop up include: "Error: package or namespace load failed."

    If you're switching R versions, we recommend creating a new library.

=== "Open OnDemand RStudio Issues"
    

=== "Linking Third Party Software"

## Using RStudio

## Example R Scripts

## Popular Packages



[^1]: The file ```~/.Renviron``` is a "dot" file which means it does not show up when you run a standard ```ls```. Files that start with a ```.``` are hidden and are typically used for important configuration information. This particular file can be used to control your R environment for each subsequent time you start a session. All the echo command does is append the line ```R_LIBS=~/R/library``` to this file. 