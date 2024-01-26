# Job Limits and Considerations

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