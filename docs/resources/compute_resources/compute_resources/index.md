# Compute Resources

## Compute Resources Available by Cluster

Before submitting a Slurm script, you must know (or at least have a general idea) of the resources needed for your job. This will tell you which type of node to request, how much memory, and other useful information that can be provided to the system via your batch script. A detailed list of Slurm batch flags are included below. 

**Node Types**

|Node Type|Description|
|-|-|
|Standard CPU Node|This is the general purpose node, designed to be used by the majority of jobs.|
|High Memory CPU Node|Similar to the standard nodes, but with significantly more RAM. There a only a few of them and they should only be requested for jobs that are known to require more RAM than is provided by standard CPU nodes.|
|GPU Node|Similar to the standard node, but with one or more GPUs available. The number of GPUs available per node is cluster-dependent.|

**Available Hardware by Cluster and Node Type**

=== "Puma"
    **Resources Available**
    
    | Node Type | Number of Nodes| CPUs/Node|RAM/CPU|CPU RAM/Node|GPUs/Node|RAM/GPU|GPU RAM/Node|Total GPUs|
    |-|-|-|-|-|-|-|-|-|
    |Standard|236|94|5gb|470gb|-|-|-|-|
    |High Memory|3 standard<br>2 buy-in| 94|32gb|3008gb|-|-|-|-|-|
    |GPU|8 standard<br>7 buy-in|94|5gb|470gb|4|32gb|128gb|32 standard<br>28 buy-in|
    
    
=== "Ocelote"
    | Node Type | Number of Nodes| CPUs/Node|RAM/CPU|CPU RAM/Node|GPUs/Node|RAM/GPU|GPU RAM/Node|Total GPUs|
    |-|-|-|-|-|-|-|-|-|
    |Standard|400|28|6gb|168gb|-|-|-|-|
    |High Memory|1| 48|41gb|1968gb|-|-|-|-|
    |GPU|46|28|8gb|224gb|1|16gb|16gb|46|
    
=== "ElGato"
    | Node Type | Number of Nodes| CPUs/Node|RAM/CPU|CPU RAM/Node|
    |-|-|-|-|-|
    |Standard|130|16|4gb|64gb|


## Job Memory and CPU Count

<div style="float: right; width: 0px; height: 100px"></div>
<div style="float: right; clear: right"><iframe width="420" height="280" src="https://www.youtube.com/embed/_dpbUqZ7rRk" allowfullscreen></iframe></div>

**Job Memory and CPU Count are Correlated**

The memory your job is allocated is dependent on the number of CPUs you request.

For example, on Puma standard nodes, you get 5G for each CPU you request. This means a standard job using 4 CPUs gets 5G/CPU × 4 CPUs = 20G of total memory. Each node has its own memory ratio that's dependent on its total memory ÷ total number of CPUs. A reference for all the node types, the memory ratios, and how to request each can be found in the Node Types/Example Resource Requests section above.

**What Happens if My Memory and CPU Requests Don't Match?**

Our systems are configured to try to help when your memory request does not match your CPU count.

For example, if you request 1 CPU and 470G of memory on Puma, the system will automatically scale up your CPU count to 94 to ensure that you get your full memory requirements. This does not go the other way, so if you request less memory than would be provided by your CPU count, no adjustments are made. If you omit the ```--memory``` flag entirely, the system will use the memory ratio for the standard nodes on that cluster.

**Possible Problems You Might Encounter**

Be careful when using ```--mem-per-cpu ratio```. If you use a higher value than a standard node ratio, you may inadvertently wind up in queue for a high memory node. On Puma there are three of these machines available for standard jobs and only one on Ocelote. This means the wait times are frequently longer than those for standard nodes. If you notice your job is in queue much longer than you would expect, check your job using job-history to ensure the memory ratio looks correct.
Stick to using ```--ntasks=N``` and ```--cpus-per-task=M``` to request $N × M$ CPUs. Using the flag ```-c``` N to request CPUs has been found to cause problems with memory requests and may inadvertently limit you to ~4MB of total memory.


[^1]: Where $1\leq N \leq 4$ 