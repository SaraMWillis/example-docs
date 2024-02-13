# Software Modules

!!! tip
    Software modules are not available on the login nodes. You will need to be on a compute node to access them.

Software packages are available as modules and are accessible from the compute nodes of any of our three clusters. A software module is a tool used to manage software environments and dependencies. It allows you to easily load and unload different software packages, libraries, and compilers needed for computational tasks without conflicts. This ensures access to many specific tools, and even different versions of the same tools, without affecting the overall system configuration.

## Module Commands

!!! warning
    If multiple versions of software are available on the system, the newest is made the default. This means loading a module without specifying the version will select the most recent. We strongly recommend including version information in your module statements. This ensures that you maintain a consistent environment for your analyses in the event of a software upgrade.

|Command | Description|
|-|-|
|```module avail```| Display all the software and versions installed on the system|
|```module avail <module_name>```|Display all installed versions of the software ```<module_name>```|
|```module list```|Display the software you have loaded in your environment|
|```module whatis <module_name>```|Displays some descriptive information about a specific module|
|```module show <module_name>```|Displays system variables that are set/modified when loading module ```<module_name>```|
|```module load <module_name>```|Load a software module in your environment|
|```module unload <module_name>```|Unload a specific software package from your environment|
|```module swap <module_name>/<version1> <module_name>/<version2>```| Switch versions of a software module|
|```module purge```| Unload all the software modules from your environment|
|```module help```| Display a help menu for the module command|

### Example
```
[netid@cpu39 ~]$ module avail python

------------------- /opt/ohpc/pub/modulefiles --------------------
   python/3.6/3.6.5     python/3.9/3.9.10
   python/3.8/3.8.2     python/3.11/3.11.4 (D)
   python/3.8/3.8.12
[netid@cpu39 ~]$ module load python/3.9
[netid@cpu39 ~]$ python3 --version
Python 3.9.10
[netid@cpu39 ~]$ module swap python/3.9 python/3.11

The following have been reloaded with a version change:
  1) python/3.9/3.9.10 => python/3.11/3.11.4

[netid@cpu39 ~]$ python3 --version
Python 3.11.4
```


## Compilers

Puma, Ocelote, and El Gato all run CentOS7 and have the following compilers available:

|Compiler|Version|Module Command|
|-|-|-|
|Intel|2020.1|```module load intel/2020.1```|
|Intel|2020.4|```module load intel/2020.4```|
|gcc|5.4.0|```module load gnu/5.4.0```|
|gcc|7.3.0|```module load gnu7/7.3.0```|
|gcc|8.3.0|```module load gnu8/8.3.0 # Loaded by default```|

## Installing additional software

To submit a request to have software installed on the UArizona HPC systems, use our [HPC Software Install Request form](https://uarizona.service-now.com/sp?id=sc_cat_item&sys_id=102d93a71ba720107947edf1604bcb55&sysparm_category=84d3d1acdbc8f4109627d90d6896191f). There is no expected time frame for how long it takes to install software, there are many variables that determine this. If you haven't heard back in a week, it is reasonable for you to follow up with a support ticket

You may also install software packages into the space that is allocated to you with your HPC account.  However, you cannot install software that requires root permission or use a method like "yum install" that accesses system paths. For information on installing software locally, see our online guide for an example.


