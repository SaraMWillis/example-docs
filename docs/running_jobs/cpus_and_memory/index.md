# CPUs and Memory

## CPU and Memory Correlation

Before submitting your job to the scheduler, it's important to know that the number of CPUs you allocate to your job determines the amount of memory you receive. 

{==Each cluster has a fixed amount of memory per CPU based on the node type==}. Accepted values by cluster and node type are listed below:

|Cluster|Standard Node|High-Memory Node|GPU Node|
|-|-|-|-|
|Puma| 5 Gb | 32 Gb | 5 Gb|
|Ocelote| 6 Gb | 41 Gb | 8 Gb|
|El Gato| 4 Gb | - | -|


For example, using the table above we can see on Puma standard nodes you get 5G for each CPU you request. This means a standard job using 4 CPUs gets 5G/CPU × 4 CPUs = 20G of total memory.

The video below shows the relationship between memory and CPUs, specifically looking at one of our Puma nodes. 

<center>
<iframe width="420" height="280" src="https://www.youtube.com/embed/_dpbUqZ7rRk" allowfullscreen></iframe>
</center>

## Determining Job Resources

The following flowchart describes the process of determining the amount of memory and number of CPUs to allocate to a job. For simplicity, this shorthand will be used:

- **N**: number of CPUs desired
- **M**: total memory desired
- **MpC**: the default value of memory per CPU for fixed cluster and node type as listed in the table above

_If a decimal value is encountered, round **up** in all cases._ 

``` mermaid
graph LR
   A[Is my job CPU<br>or Memory limited?] 
   B["`set CPUs=**N**`"]
   C["`do not specify
   memory or mem/cpu`"]
   D["`Set CPUs=**M**/**MpC**`"]
   E["`Set mem/CPU=**MpC**`"]
   Z[Done]
   A -->|CPU| B --> C --> Z
   A -->|mem| D -.-> E --> Z
   D --> Z
```

The dotted line above indicates that setting mem/CPU in your job is not strictly necessary. If you are requesting a standard node, this value is set for you by the scheduler. The only times you will need to set this value is:

1. If you're requsting a non-standard node (e.g. a high memory or Ocelote GPU node)
2. If you're requesting an OnDemand application session. There is a field where you will fill in your mem/CPU requirement. 

Note that there is no deterministic method of finding the exact amount of memory needed by a job _in advance_. A general rule of thumb is to overestimate it slightly and then scale down based on previous runs. Massive overestimation, however, can lead to inefficiency of system resources and unnecessary expenditure of CPU time allocations. 

## Things to Watch out for

- **Invalid Values**

    Be careful when requesting memory and memory per CPU. Note that if you request invalid mem/cpu values, unpredictable results may occur:
        1. You may may be put in queue for a high memory node which have significantly longer wait times.
        2. You may receive less memory than expected

- **Memory and CPU Mismatches**

    In the case of batch script: if you request memory instead of memory/CPU, the scheduler will automatically bump up your CPU allocation to match your memory requirements if there is a mismatch. This means, for example, if you were to request one CPU and 50 GB of total memory, the scheduler would allocate 10 CPUs to your job.  

- **Invalid Mem/CPU Options**

    If you request a mem/CPU value that is invalid, the scheduler will not reject it and will try to accomodate your request. This may mean your job will be bumped to the high memory node if you request more than the standard ratio. It may also mean you'll get less memory than expected.