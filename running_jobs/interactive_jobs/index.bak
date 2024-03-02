# Interactive Jobs

## Overview

Interactive sessions are a way to gain access to a compute node from the command line. This is useful for checking available modules, testing submission scripts, compiling software, and running programs in real time. When you are on a login node, you can request a session by simply entering: ```interactive```. For example:

```bash
(ocelote) [netid@junonia ~]$ interactive
Run "interactive -h for help customizing interactive use"
Submitting with /usr/local/bin/salloc --job-name=interactive --mem-per-cpu=4GB --nodes=1    --ntasks=1 --time=01:00:00 --account=windfall --partition=windfall
salloc: Pending job allocation 531843
salloc: job 531843 queued and waiting for resources
salloc: job 531843 has been allocated resources
salloc: Granted job allocation 531843
salloc: Waiting for resource configuration
salloc: Nodes i16n1 are ready for job
[netid@i16n1 ~]$
```

Notice in the example above how the command prompt changes once your session starts. When you're on a login node, your prompt will show "junonia" or "wentletrap". Once you're in an interactive session, you'll see the name of the compute node you're connected to. 

## Customizing Your Resources

The command ```interactive``` when run without any arguments will allocate you a windfall session using one CPU for one hour which isn't ideal for most use cases. You can modify this by including additional flags. To see the available options, you can use the help flag ```-h```

```bash
(ocelote) [netid@junonia ~]$ interactive -h
Usage: /usr/local/bin/interactive [-x] [-g] [-N nodes] [-m memory per core] [-n total number of tasks] [-Q optional qos] [-t hh::mm:ss] [-a account to charge]
```
The values can be combined and each mean the following:

|Flag|Explanation|<div style="width:150px">Example</div>|
|-|-|-|
|```-a```|This is followed by your group's name and will switch you to using the standard partition. This is highly recommended to keep your sessions from being interrupted and to help them start faster|```-a my_group```|
|```-t```|The amount of time to reserve for your job in the format ```hhh:mm:ss```|```-t 05:00:00```|
|```-n```|Total number of tasks (CPUs) to allocate to your job. By default, this will be on a single node|```-n 16```|
|```-N```|Total number of nodes (physical computers) to allocate to your job|```-N 2```|
|```-m```|Total amount of memory **per CPU**. See [Compute Resources](/running_jobs/compute_resources/#compute-resources-available-by-cluster) for more information and potential complications|```-m 5gb```|
|```Q```|Used to add a qos to access high priority or qualified hours. Only for groups with buy-in/special project hours|```-Q user_qos_pi_netid```|
|```-g```|Request a GPU. This flag takes no arguments. If you want to request more than one GPU in an interactive session, you can use [salloc](/running_jobs/batch_jobs/slurm_documentation/) directly|```-q```|
|```-x```|Enable [X11 forwarding](/registration_and_access/system_access/#x11-forwarding). This flag takes no arguments.|```-x```|

You may also create your own salloc commands using any desired Slurm directives for maximum customization.


## Tips and Tricks for Faster Sessions

* **Switch to ElGato** 
    
    This cluster shares the same operating system, software, and file system as Puma so often your workflows are portable across clusters. Ocelote and ElGato standard nodes have 28 and 16 CPUs, respectively, and are often less utilized than Puma meaning much shorter wait times. Before you run the interactive command, type elgato to switch.
    
* **Use the account flag**
    
    By default, ```interactive``` will request a session using the windfall partition. Windfall is lower priority than standard and so these types of jobs take longer to get through the queue. If you include the account flag, that will switch your partition to standard. An example of this type of request:
    ```bash
    interactive -a YOUR_GROUP
    ```