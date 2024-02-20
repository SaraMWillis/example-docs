# Secure HPC Overview

!!! warning
    Currently Soteria is in a pilot test mode and is not generally available. It is expected that the testing will run until the middle of 2023 

Research Technologies in partnership with the Data Science Institute is providing a secure research enclave that is HIPAA compliant. It is called Soteria. In Greek mythology, Soteria (Greek: Σωτηρία) was the goddess or spirit (daimon) of safety and salvation, deliverance, and preservation from harm.

Soteria will be available for access using the OnDemand graphical interface.

## Available Resources

This small HPC cluster has many of the capabilities of the main HPC.  There are compute nodes, with the same core count and memory. And there are two GPU nodes.

This small cluster has four standard compute nodes. Each has 94 cores and 512GB memory available. The two GPU nodes have the same resources but there are also four V100 GPU's in each. You can use the regular parts of the documentation to learn how to use slurm with these nodes.
In case you are interested, these nodes are named by their physical location and you will see this if you are connected to an interactive session. And with OnDemand (OOD) your connection will show the node hostname.

|Node Type|Node Names|
|-|-|
|Standard Nodes| r1u26n1,r1u27n1,r1u28n1,r1u29n1|
|GPU Nodes| r1u30n1,r1u32n1|

## Allocations and Storage

For the purpose of this early testing, the allocations of time and space will be similar to HPC.
The time allocation will be 100,000 hours.
Your account will come with space in ```/home``` and ```/groups``` where you can put your data.  Currently those directories are not subject to a quota limit.

