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
    |Standard|192 standard<br>108 buy-in|94|5gb|470gb|-|-|-|-|
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


## Technical Specifications

||ElGato|Ocelote|Puma|
|-|-|-|-|
|Model|IBM System X iDataPlex dx360 M4|Lenovo NeXtScale nx360 M5|Penguin Altus XE2242|
|Year Purchased|2013|2016 (2018 P100 nodes)|2020|
|Node Count|118|373 CPU-only<br>46 GPU<br>1 High Memory|300 CPU-only<br>15 GPU<br>5 High Memory<br>|
|Total System Memory|26TB|82.6TB|128TB|
|Processors|2x Xeon E5-2650v2 8-core (Ivy Bridge)|2x Xeon E5-2695v3 14-core (Haswell)<br>2x Xeon E5-2695v4 14-core (Broadwell)<br>4x Xeon E7-4850v2 12-core (Ivy Bridge)|2x AMD EPYC 7642 48-core (Rome)|
|Cores/Node (Schedulable)|16c|28c (48c - High-memory node)|94c|
|Total Cores|1888|11696[^1]|30720[^1]|
|Processor Speed|2.66GHz|2.3GHz (2.4GHz - Broadwell CPUs)|2.4GHz|
|Memory/Node|256GB - GPU nodes<br>64GB - CPU-only nodes|192GB (2TB - High-memory node)|512GB (3TB - High-memory nodes)|
|Accelerators|46 NVIDIA P100 (16GB)|29 NVIDIA V100S|
|/tmp[^2]|~840 GB spinning|~840 GB spinning|~1440 TB NVMe|
|HPL Rmax (TFlop/s)|46|382||
|OS|CentOS 7|CentOS 7|CentOS 7|
|Interconnect|FDR Inifinband|FDR Infiniband for node-node<br>10 Gb Ethernet node-storage|1x 25Gb/s Ethernet RDMA (RoCEv2)<br>1x 25Gb/s Ethernet to storage|

## GPU Nodes


=== "Puma"
    <img src="images/v100_info.jpg" width=400px style="float: right; margin: 5px;">
    Puma has a different arrangement for GPU nodes than Ocelote and ElGato. Whereas the older clusters have one GPU per node, Puma has four. This has a financial advantage for providing GPU's with lower overall cost, and a technical advantage of allowing jobs that can use multiple GPU's to run faster than spanning multiple nodes.  This capability comes from using a newer operating system.  
    
    Each node has four Nvidia V100S model GPUs. They are provisioned with 32GB memory compared to 16GB on the P100's.  

=== "Ocelote"
    <img src="images/p100_info.png" width=400px style="float: right; margin: 5px;">
    Ocelote has 46 compute nodes with Nvidia P100 GPUs that are available to researchers on campus. The limitation is a maximum of 10 concurrent jobs. Previously, one node with a V100 was available, but it has since been replaced with a P100. Tasks which require multiple GPUs must either request multiple nodes on Ocelote, or use Puma's GPU nodes.

=== "ElGato"
    ElGato has no GPU nodes. During the quarterly maintenance cycle on April 27, 2022 the ElGato K20s and Ocelote K80s were removed due to no longer being supported by Nvidia.





### MIG (Multi-Instance GPU) Resources

**Overview**

The Four A100 GPUs on Puma Node r5u13n1 are each subdivided into 3 smaller virtual GPUs using the Nvidia MIG (Multi-Instance GPU) method.  Each of these MIG slices allows the use of 20 GB of GPU memory.  The vast majority of jobs run on Puma in 2023 used less than this amount of GPU memory.  The  12 MIG GPUs  will increase overall GPU availability on Puma by freeing the 32 GB V100 GPUs for users requiring larger amounts of GPU memory.

Jobs requesting MIG resources will ideally be scheduled more quickly than those requesting the standard V100 GPUs, so MIG resources should be preferred when sufficient.

A limitation is that only one MIG slice can be addressed by a single application, so {==MIG slices are not appropriate for jobs utilizing multiple GPUs==}.

**Using MIG Resources** 

The addition of the MIG devices to the Slurm queues will have a number of impacts, and some users may need to make changes to submissions to ensure proper functioning of analyses. For more information on requesting GPU resources, see our [Batch Jobs](../../running_jobs/batch_jobs/batch_directives/#gpus), [Interactive Jobs](../../running_jobs/interactive_jobs/), and/or [Open OnDemand Jobs](../../running_jobs/open_on_demand/) guides. 





[^1]: Includes high-memory and GPU node CPUs
[^2]: /tmp is scratch space and is part of the root filesystem