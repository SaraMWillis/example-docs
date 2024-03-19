<link rel="stylesheet" href="../../assets/stylesheets/buttons.css">
# Common Misconceptions

Both experienced and novice users may benefit from reading through these common misconceptions. 

### **If I move my code to HPC, it will automatically run faster**

You might be surprised to learn that if you move code from a local computer to a supercomputer, it will not automatically run faster and may even run *slower*. This is because the power of a supercomputer comes from the volume of resources available (compute nodes, CPUs, GPUs, etc.) and not the clockspeed of the processors themselves. Performance boosts come from optimizing your code to make use of the additional processors available on HPC, a practice known as parallelization.

Parallelization enables jobs to 'divide-and-conquer' independent tasks within a process. A classic example of the advantages of parallel computing is multiplying an $N \times N$ matrix by a scalar, which takes $N^2$ floating-point operations (flops). On one CPU, this will take an amount of time $t = N^2 / f$ where $f$ is the clock frequency of the CPU. On an integer $M$ number of CPUs, this computation will instead take $t' = \frac{t}{M}$. Most analyses involve computations which are not always as independent as matrix multiplication, leading to less than perfect speedup times. The behavior of predicted speedup time for an analysis of fixed size is known as [Strong Scaling](https://hpc-wiki.info/hpc/Scaling).

### **If I allocate more CPUs to my job, my software will use them**

Most software needs to be designed to use multiple CPUs as part of its execution. You will need to ensure your software has the capability to make use of multiple CPUs for it to be able to take advantage of additional hardware. The job scheduler only provides the resources, the code itself is what needs to know how to make use of them.

### **If I allocate more nodes (physical computers) to my job, my software will use them**
    
Similar to above, software must be designed to be able to take advantage of additional computers when they are allocated to your job. Most often, this is using something like MPI. If your software is not MPI-enabled, it cannot use more than one computer as part of its analyses, even if it is using something like OpenMP or Python multiprocessing to make use of multiple CPUs. 

### **All nodes on a supercomputer are the same**

While all compute nodes on a given cluster may have identical hardware, navigating the HPC means being aware of the different types of nodes you can land on. For example, the login node is available to all users by default upon login, and is designed for managing and editing files. However, it is not designed to run production computations. Running jobs that are to computationally intensive on the login node can severely impact performance for other users. Such jobs will be noticed and stopped by the HPC systems team.

Types of nodes on the UA HPC system include the Bastion Host, the Login Node, the Compute Nodes, and the Data Transfer Node. See [Compute Resources](../../resources/compute_resources) for more information.


### **As a user I (am)(am not) allowed to install my own software**

Well, it depends. Users can create custom environments and install packages for languages like Python and R by using their built-in package managers. Users are even encouraged to download software from github or other repositories and compile it themselves (provided it is done on a compute node). However, system-wide modules are generally taken care of by the HPC team. If you would like something to be installed as software available to all HPC users, you can make a request through [ServiceNow](https://uarizona.service-now.com/sp?id=sc_cat_item&sys_id=2983102adbd23c109627d90d689619c6&sysparm_category=84d3d1acdbc8f4109627d90d6896191f). But, if you would like something to be installed for personal use, or use between members of your group, you are encouraged to install it in one of your shares on the HPC filesystem. If you would like assistanace with the install process, you may contact the HPC Consult team through ServiceNow or [hpc-consult@list.arizona.edu](mailto:hpc-consult@list.arizona.edu) (please outline the exact steps you have taken, and include all error messages you received). 

<html>
<div class="button-container">
    <a href="../supercomputing_in_plain_english"><button class="left-button"></button></a>
    <a href="../logging_in/"><button class="right-button"></button></a>
</div>
</html>