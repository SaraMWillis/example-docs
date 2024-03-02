# Compute Resources

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





[^1]: Where $1\leq N \leq 4$ 