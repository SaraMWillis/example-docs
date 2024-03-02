# Partition Requests

!!! tip
    To find your group name and allocation, use the command ```va```


## Batch Jobs

Slurm uses the ```--partition``` directive to determine which [allocation](../../allocations/) to charge. When using any partition other than windfall, the account associated with the allocation must be specified. Non-standard partitions including high-priority and special projects must also specify a ```--qos``` (quality of service) directive. An example of each use case is shown below. 

|Partition|Job Directives|
|-|-|
|Standard|<pre><code>#SBATCH --account=PI_GROUP<br>#SBATCH --partition=standard</code></pre>|
|Windfall|<pre><code>#SBATCH --partition=windfall</code></pre>|
|High Priority[^1]|<pre><code>#SBATCH --account=PI_GROUP<br>#SBATCH --partition=high_priority<br>#SBATCH --qos=user_qos_PI_GROUP</code></pre>|
|Qualified|<pre><code>#SBATCH --account=PI_GROUP<br>#SBATCH --partition=qualified<br>#SBATCH --qos=qual_qos_PI_GROUP</code></pre>|

[^1]: The high priority partition only exists on Puma