# Linux Cheat Sheet

## Why Learn Bash

Bash is a powerful command line shell that allows you to interact with our systems efficiently. It enables scripting and automation, job submission, file and directory management, remote access, resource monitoring, environment customization, parallel computing, data preprocessing, version control, error handling, software dependency management, custom workflows, and offers a valuable skill set applicable beyond HPC tasks. In other words, it allows you to do a lot!

In the cheat sheet below, we offer some basics as a reference. We also highly suggest you explore some more comprehensive guides such as the following: [Introduction to Linux on HPC](../workshops/intro_to_linux/)

## Shell Basics

### Shortcuts
Shortcuts are used as standins 
|Shortcut|Description|
|-|-|
|```~```|Your home directory|
|```.```|Your working directory|
|```..``` One directory above your working directory|

### Commands


|```ls```|List the contents of a directory|
|-|-|
|```ls -la```|List the contents of a directory including hidden files|
|```cd```|Change your working directory|
|```pwd```|Show the path to your working directory|
|```mkdir```|Create a new directory|
|```rm```| Delete a file. **Be careful**, files deleted this way **can't be retrieved**|
|```rm -r```|Delete a directory. **Be careful**, directories deleted this way **can't be retrieved**|

## Hidden Files and Directories
Hidden files and directories start with a dot ```.``` and won't show up when you do a simple ```ls```. Some of these files are used to configure your environment when you first log in. Be careful when removing or modifying these files since doing so can cause unintended consequences.

|File/Directory|What It Does|Warnings|
|-|-|-|
|```~/.bash_profile```|	This file sets your working environment when you first log into HPC. This file sources your ```~/.bashrc``` (see below).|Removing this file will result in the loss of the module command|
|```~/.bashrc```|This file sets your working environment when you first log into HPC. Modifying this script|Removing this file will result in the loss of the module command|
|```~/.local```|This is a hidden directory in your home where pip-installed python packages, jupyter kernels, RStudio session information, etc. goes.|If you pip-install python packages when a virtual environment is not active, they will be installed in this directory. These will then be automatically loaded for all future python sessions (version-specific), including in Singularity images. This may cause versioning issues. We recommend always using [virtual environments](../../software/popular_software/python_and_anaconda/python/).|
|```~/.apptainer```|A hidden directory in your home where Apptainer images and cache files are stored by default.|This directory can grow large quickly and fill up your home. You can modify your ```~/.bashrc``` to [set a different cache directory location](../../software/containers/containers_on_hpc/) that has a larger quota.

## Environment Variables

### Overview
These are important bash variables that control how your environment is configured. For example: what executables, libraries, header files, etc. are findable by default; information about your Slurm job; MPI settings; GPU configuration; etc. To see all the environment variables that are defined for your session, try running the command ```env```.

## Linux File Permissions

Linux file permissions control who can access files and directories and what they are able to do with them.

HPC users may find it useful or necessary to share files and/or directories with collaborators. To do this effectively, it may become necessary to familiarize yourself with the linux file permission system in order to give collaborators access to your files. 

### Types of Permissions

All files and directories on a Linux system have permissions defined for them. There are three types:

|Permission|Symbol|Directory meaning|File meaning|
|-|-|-|-|
|Read|```r```|Users can view the contents of the directory|Users can read the contents of a file|
|Write|```w```|Users can modify the contents of a directory|Users can write to a file|
|Execute|```x```|Users can ```cd``` into a directory|Users can directly execute a file|

When a permission is missing, you will see a ```-```


### Viewing Permissions
To see a file or directory's file permissions, run the command ```ls -l```. This will show you output that looks like the following:

<center><code style="background-color: #faca89;">-</code><code style="background-color: #fff0bf;">rwx</code><code style="background-color: #deffbf;">r-x</code><code style="background-color: #bffff6;">---</code><code> 1 </code><code style="background-color: #fff0bf;">username</code><code> </code><code style="background-color: #deffbf;">groupname</code><code> 0 Feb 27 09:54 file</code></center>

|String|Access Group|Meaning|
|-|-|-|
|<code style="background-color: #faca89;">-</code>|Tells you whether this item is a regular file (```-```), directory (```d```), or link ```(l)```|In this example, we're looking at a regular file|
|<code style="background-color: #fff0bf;">rwx</code>|This describes the permissions that are set at the user level. In this case, they apply to the user with the username <code style="background-color: #fff0bf;">username</code>. Your username is your NetID| In this example, the file's owner can read, modify, and execute this file.|
|<code style="background-color: #deffbf;">r-x</code>|This describes the permissions that are set at the group level. In this case, they apply to anyone who is a member of the group <code style="background-color: #deffbf;">groupname</code>. To see your groups you're a member of, run the command ```groups```.|In this example, group members are allowed to see and execute the contents of this file, but they cannot modify it. 
|<code style="background-color: #bffff6;">---</code>|This describes the permissions that are set for anyone else on the system.|In this example, the rest of the HPC community can't see or edit the contents of this file and can't execute it|

### Changing Permissions

To change the permissions of a file or directory, you can use the command ```chmod```. This accepts two types of input: symbolic and octal.

**Symbolic**

Symbolic notation is the most intuitive to understand. It involves a comma-delimited list of 

### Changing Group Ownership

!!! tip
    Users can't change the user ownership of a file. This is because this requires administrator privileges. User ownership changes can be requested from our consulting team. 

To change the group ownership of a file or directory, you can use ```chgrp```. For example:

```
chgrp groupname /path/to/file
```

## Compression and Archiving 

Are you planning on transferring files to or from HPC? Do you have a lot of them? Then archiving is for you! 

Archiving files is the process of consolidating one or more files or directories into a single, compressed package or archive file. This simplifies data management, reduces storage space, and streamlines file transfer and backup operations. Transferring a single archived file to an external backup location my result in transfer speeds that are an order of magnitude faster than transferring the same data as an uncompressed directory with thousands (or sometimes millions) of files.

As an example, we'll use the archiving tool ```tar```. The syntax to create an archive is ```tar <options> <output_archive_name> <contents>```. We'll use the options ```czvf``` which stands for:

* ```c```: Create a new archive
* ```z```: Filter the archive through gzip
* ```v```: Verbosely print the output of the archiving process. Optional
* ```f```: User archive file

Archiving a directory ```dir``` and its contents into a single file called ```dir.tar.gz``` then looks like:

```
(puma) [user@wentletrap archiving_example]$ tar czvf dir.tar.gz dir
dir/
dir/subdir1/
dir/subdir1/file.txt
dir/file1.txt
dir/file3.txt
dir/file2.txt
(puma) [user@wentletrap archiving_example]$ ls
dir  dir.tar.gz
```

To unpack this archive, change the ```c``` to an ```x``` which stands for "extract":

```
tar xzvf dir.tar.gz
```