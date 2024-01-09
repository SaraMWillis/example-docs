# UArizona HPC Documentation

## Our Mission
UA High Performance Computing (HPC) is an interdisciplinary research center focused on facilitating research and discoveries that advance science and technology. We deploy and operate advanced computing and data resources for the research activities of students, faculty, and staff at the University of Arizona. We also provide consulting, technical documentation, and training to support our users.

This site is divided into sections that describe the High Performance Computing (HPC) resources that are available, how to use them, and the rules for use.



## Quick Links
<div class="grid" markdown>

[:material-web: __Open OnDemand__](https://ood.hpc.arizona.edu/)
{ .card }

[:material-account: __User Portal__](https://portal.hpc.arizona.edu/)
{ .card }

[:fontawesome-brands-youtube: Training Videos](https://www.youtube.com/@universityofarizonauitsres7597)
{ .card }

[:material-comment-question: Getting Help](/support_and_training/consulting_services/)
{.card}

</div>

## Our Clusters

=== "Puma"

    <div style="float: right; width: 0px; height: 100px"></div>
    <div style="float: right; clear: right"><img width="300" src="home/images/puma.jpg"></div>
    
    Implemented in 2020, Puma is the biggest cat yet. Similar to Ocelote, it has standard CPU nodes (with 94 cores and 512 GB of memory per node), GPU nodes (with Nvidia V100) and two high-memory nodes (3 TB). Local scratch storage increased to ~1.4 TB. Puma runs on CentOS 7.
    
    |Puma Technical Specifications||
    |-|-|
    |Model|Penguin Altus XE2242|
    |Year Purchased|2020|
    |Node Count|236 CPU-only<br>8 GPU<br>3 High-memory|
    |Total System Memory (TB)|128TB|
    |Processors|2x AMD EPYC 7642 48-core (Rome)|
    |Cores/Node (Schedulable)|94c|
    |Total Cores|23616*|
    |Processor Speed|2.4GHz|
    |Memory Per Node|512GB (3TB - High-memory nodes)|
    |Accelerators|29 NVIDIA V100S|
    |```/tmp```|~1440 TB NVMe<br>```/tmp``` is part of root filesystem|
    |HPL Rmax (TFlop/s)||
    |OS|CentOS 7|
    |Interconnect|1x 25Gb/s Ethernet RDMA (RoCEv2)<br>1x 25Gb/s Ethernet to storage|
    

=== "Ocelote"

    <div style="float: right; width: 0px; height: 100px"></div>
    <div style="float: right; clear: right"><img width="300" src="home/images/ocelote.jpg"></div>
    
    Implemented in the middle of 2016, Ocelote is designed to support the majority of workloads on the standard nodes. Additionally, Ocelote has one large memory  node with 2TB of memory and 46 nodes with Nvidia P100 GPUs for GPU-accelerated workflows
    
    |Ocelote Technical Specifications||
    |-|-|
    |Model|Lenovo NeXtScale nx360 M5|
    |Year Purchased|2016 (2018 P100 nodes)|
    |Node Count|400|
    |Total System Memory (TB)|82.6TB|
    |Processors|2x Xeon E5-2695v3 14-core (Haswell)<br>2x Xeon E5-2695v4 14-core (Broadwell)<br>4x Xeon E7-4850v2 12-core (Ivy Bridge)|
    |Cores/Node (Schedulable)|28c (48c - High-memory node)|
    |Total Cores|11528*|
    |Processor Speed|2.3GHz (2.4GHz - Broadwell CPUs)|
    |Memory Per Node|192GB (2TB - High-memory node)|
    |Accelerators|46 NVIDIA P100 (16GB)|
    |```/tmp```|~840 GB spinning<br>```/tmp``` is part of root filesystem|
    |HPL Rmax (TFlop/s)|382|
    |OS|CentOS 7|
    |Interconnect|FDR Infiniband for node-node<br>10 Gb Ethernet node-storage|
    |* Includes high-memory and GPU node CPU

=== "ElGato"

    <div style="float: right; width: 0px; height: 100px"></div>
    <div style="float: right; clear: right"><img width="300" src="home/images/elgato_jones.jpg"></div>

    Implemented at the start of 2014, ElGato has been reprovisioned with CentOS 7 and new compilers and libraries. From July 2021 it has been using Slurm for job submission. ElGato is our smallest cluster with 130 standard nodes each with 16 CPUs. Purchased by an NSF MRI grant by researchers in Astronomy and SISTA.
    
    |ElGato Technical Specifications||
    |-|-|
    |Model|IBM System X iDataPlex dx360 M4|
    |Year Purchased|2013|
    |Node Count|131|
    |Total System Memory (TB)|26TB|
    |Processors|2x Xeon E5-2650v2 8-core (Ivy Bridge)|
    |Cores/Node (Schedulable)|16c|
    |Total Cores|2160*|
    |Processor Speed|2.66GHz|
    |Memory Per Node|256GB - GPU nodes<br>64GB - CPU-only nodes|
    |Accelerators||
    |```/tmp```|~840 GB spinning<br>```/tmp``` is part of root filesystem|
    |HPL Rmax (TFlop/s)|46|
    |OS|CentOS 7|
    |Interconnect|FDR Inifinband|
    |* Includes high-memory and GPU node CPU|


<div style="float: right; width: 0px; height: 100px"></div>
<div style="float: right; clear: right"><img width="300" src="home/images/HypersonicTravel.jpg"></div>


## Highlighted Research

**Faster Speeds Need Faster Computation**

**Hypersonic Travel**

Professors Christoph Hader, Hermann Fasel, and their team are exploring the use of our GPUs to optimize Navier-Stokes codes for simulating the flow field around hypersonic vehicles traveling at size times the speed of sound (Mach 6) or more. 

In the image to the right, instantaneous flow structures obtained from a DNS for a flared cone at Mach 6 are visualized using the Q-isocontours colored with instantaneous temperature disturbance values. The small scales towards the end of the computational domain indicate the regions where the boundary layer is turbulent. 

## HPC Data Center Tour

You may not get to see the actual supercomputers where your work is done, but you can watch this tour. Note how loud it is in the room. The video does not convey the temperature of the room, but there are no warm areas. As you will hear explained, the cooling is done with chilled water.

<center><iframe src="https://www.youtube.com/embed/JOJ8RO4tLcc" allowfullscreen width=600 height="400"></iframe></center>


<br> <hr>

<div style="text-align: center; color: dark grey; font-size: 12px;">
    We respectfully acknowledge the University of Arizona is on the land and territories of Indigenous peoples. Today, Arizona is home to 22 federally recognized tribes, with Tucson being home to the O'odham and the Yaqui. Committed to diversity and inclusion, the University strives to build sustainable relationships with sovereign Native Nations and Indigenous communities through education offerings, partnerships, and community service.
</div>
