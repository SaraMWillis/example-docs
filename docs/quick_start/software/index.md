<link rel="stylesheet" href="../../assets/stylesheets/buttons.css">
# Software on HPC

It's hard to perform analyses without software. We learned that software packages are not available on the login nodes, but now that we're connected to a compute node, we can see and use what's available. 

Software on HPC comes [installed as modules](../../software/modules/). Modules make it easy to load and unload software from your environment. This allows hundreds of packages to be available on the same system without dependency or versioning conflicts. It's always good practice to specify which version of the software you need when loading to ensure a stable environment.

You can view and load software modules using the commands ```module avail``` and ```module load```, respectively. For example:

```
[netid@gpu66 ~]$ module avail python
 
------------------------------------------------- /opt/ohpc/pub/modulefiles --------------------------------------------------
   python/3.6/3.6.5    python/3.8/3.8.2 (D)    python/3.8/3.8.12    python/3.9/3.9.10
 
[netid@gpu66 ~]$ module load python/3.9
[netid@gpu66 ~]$ python3 --version
Python 3.9.10
```

Try running ```module avail``` without specifying any arguments. You'll notice we have *a lot* available.

Since you're in an interactive session, you have exclusive access to the resources you've reserved which means you can use this software to develop, test, run, and debug your code. Interactive sessions are optimal for these sorts of actions. However, you might run into problems executing your analyses if:

* Your session times out due to inactivity
* Your internet connection gets disrupted
* Your computer gets closed or turned off
* You want to run more than one job at a time

That's where batch jobs come in. 

<html>
<div class="button-container">
    <a href="../interactive_jobs"><button class="left-button"></button></a>
    <a href="../batch_jobs/"><button class="right-button"></button></a>
</div>
</html>