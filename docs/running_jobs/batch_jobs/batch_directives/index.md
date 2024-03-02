# Batch Directives

!!! tip
    For a full list of directives, see [Slurm's official documentation](https://slurm.schedmd.com/sbatch.html).

The topmost section of a batch script always contains the [Slurm Directives](https://slurm.schedmd.com/ "slurm.schedmd.com"), which specify the resource requests for your job, which the scheduler then parses in order to allocate CPUs, memory, walltime, etc.

Below are important directives to include in any script that will control the resources you're allocated and your job's priority:
 
## Partitions

!!! warning "Limited Availability"
    <mark>The **high-priority** and **qualified partitions** are **limited access**.</mark> High-priority is only available to PI groups which participated in the Puma [buy-in](../../../policies/buy_in/) process, which has since concluded. Qualified is available to PI groups which have been granted [special projects](../../../policies/special_projects/). 

There are four available partitions on the UArizona HPC. With the exception of Windfall, these consume your monthly allocation. See our [allocations documentation](../../../resources/allocations/) for more information on each. The syntax to request each of the following is shown below:


|Partition|Priority|Account|QOS|Cost|Slurm|
|-|-|-|-|-|-|
|Standard|normal|required|n/a|normal|<pre><code>#SBATCH --account=&lt;PI GROUP&gt;<br>#SBATCH --partition=standard</code></pre>|
|Windfall|low|exclude|n/a|none|<pre><code>#SBATCH --partition=windfall</code></pre>|
|High Priority|high|required|required|normal|<pre><code>#SBATCH --account=&lt;PI GROUP&gt;<br>#SBATCH --partition=high_priority<br>#SBATCH --qos=user_qos_&lt;PI GROUP&gt;</code></pre>|
|Qualified|normal|required|required|normal|<pre><code>#SBATCH --account=&lt;PI GROUP&gt;<br>#SBATCH --partition=standard<br>#SBATCH --qos=qual_qos_&lt;PI GROUP&gt;</code></pre>|

## Nodes

!!! danger
    In order for your job to make use of more than one node, it must be able to make use of something like MPI. If your application is non-MPI enabled, always set ```--nodes=1```

The term nodes is synonymous with the number of physical computers allocated to your job. The syntax to allocate ```N``` nodes to a job is:

```
#SBATCH --nodes=N
```

## CPUs

Each job must specify the number of CPUs they need for their application with the ```--ntasks``` directive.  This can be done in one of two ways:

1. If your application is making use of MPI or is executing simultaneous distinct processes, you can request ```N``` CPUs with

    ```bash
    #SBATCH --ntasks=N
    ```

2. If you are using a multithreaded application, then you can request ```N``` CPUs with:
    ```bash
    #SBATCH --ntasks=1
    #SBATCH --cpus-per-task=N
    ```

## Memory and High Memory Nodes

!!! tip
    More detailed information on memory and CPU requests can be found on our [CPUs and Memory page](../../cpus_and_memory/).

Memory is an optional flag. By default, the scheduler will allocate you the [standard CPU/memory ratio](../../cpus_and_memory/) available on the cluster. 

Memory can either be requested with the ```--mem``` or ```--mem-per-cpu``` flags. The ```--mem``` flag indicates the amount of {==Memory per **node**==} to allocate to your job and *not* the total memory. If you are running multi-node MPI jobs with this flag, the total amount of memory you will receive will be ```mem```$\times$```nodes```

```
#SBATCH --mem=Ngb
```
or
```
#SBATCH --mem-per-cpu=Ngb
```

**High Memory Node Requests**

To request a high memory node, you will need the additional flag ```--constraint=high_mem```

|Cluster|Command|
|-|-|
|Ocelote|<pre><code>#SBATCH --mem-per-cpu=41gb<br>#SBATCH --constraint=high_mem</code></pre>|
|Puma|<pre><code>#SBATCH --mem-per-cpu=32gb<br>#SBATCH --constraint=high_mem</code></pre>|




## GPUs (Optional)

For an overview of the GPU resources available on each cluster, see our [resources documentation](../../../resources/compute_resources/gpu_nodes/). 

<table>
  <colgroup>
    <col style="width: 10%;">
    <col style="width: 50%;">
    <col style="width: 40%;">
  </colgroup>
  <tr>
    <th>Cluster</th>
    <th>Directive</th>
    <th>Target</th>
  </tr>
  <tr>
    <td rowspan=3  style="vertical-align: middle;">Puma</td>
    <td><code>#SBATCH --gres=gpu:1</code></td>
    <td>Request a single GPU. This will either target one Volta GPU (v100) or one A100 MIG slice, depending on availability. Only one GPU should be selected with this method to avoid being allocated multiple MIG slices.</td>
  </tr>
  <tr>
    <td><code>#SBATCH --gres=gpu:nvidia_a100_80gb_pcie_2g.20gb</code></td>
    <td>Target one A100 MIG slice.</td>
  </tr>
  <tr>
    <td><code>#SBATCH --gres=gpu:N</code></td>
    <td>Request <code>N</code> V100 GPUs. Up to four may be requested on a node.</td>
  </tr>
  <tr>
    <td>Ocelote</td>
    <td><code>#SBATCH --gres=gpu:1</code></td>
    <td>Request 1 Pascal GPU (p100)</td>
</table>

## Time

The syntax for requesting time for your job is HHH:MM:SS or DD-HHH:MM:SS

```
#SBATCH --time=HHH:MM:SS
```



## Additional Directives
|<div style="width:270px">Command</div>|Purpose|
|-|-|
|```#SBATCH --job-name=JobName```|Optional: Specify a name for your job. This will not automatically affect the output filename.|
|```#SBATCH -e output_filename.err```<br>```#SBATCH -o output_filename.out```|Optional: Specify output filename(s). If ```-e``` is missing, stdout and stderr will be combined.|
|```#SBATCH --open-mode=append```|Optional: Append your job's output to the specified output filename(s).```
|```#SBATCH --mail-type=BEGIN|END|FAIL|ALL```|Optional: Request email notifications. **Beware of mail bombing yourself.**|
|```#SBATCH --mail-user=email@address.xyz```|Optional: Specify email address. If this is missing, notifications will go to your UArizona email address by default.|
|```#SBATCH --export=VAR```|Optional: Export a comma-delimited list of environment variables to a job.|
|```#SBATCH --export=all```|Optional: Export your working environment to your job. This is the default.|
|```#SBATCH --export=none```|Optional: Do not export working environment to your job.|














## Examples and Explanations

The below examples are _complete_ sections of Slurm directives that will produce valid requests. Other directives can be added (like output files), but they are not strictly necessary to submit a valid request. For simplicity, the Puma cluster is assumed when discussing memory and GPU resources. Note that these examples do not include the shebang ```#!bin/bash``` statement, which should be at the top of _every_ slurm script. Also, note that the order of directives does not matter.

=== "Single CPU"
    ```
    #SBATCH --job-name=hello_world
    #SBATCH --account=your_group
    #SBATCH --partition=standard
    #SBATCH --nodes=1
    #SBATCH --ntasks=1
    #SBATCH --time=01:00:00
    ```

    This example requests one CPU on one node for one hour. Easy!

=== "Single Node"
    ```
    #SBATCH --job-name=hello_world
    #SBATCH --account=your_group
    #SBATCH --partition=standard
    #SBATCH --nodes=1
    #SBATCH --ntasks=10
    #SBATCH --time=01:00:00
    ```

    10 CPUs are now requested. The default value of ```mem-per-cpu``` is assumed, therefore giving this job 50gb of total memory. Specifying this value by including ```#SBATCH --mem-per-cpu=5gb``` will not change the behavior of the above request. If ```#SBATCH --mem-per-cpu=10gb``` is included (for example), a high-memory node will be requested instead. Please only include values from the above table for the ```mem-per-cpu``` option. 

    The example below will produce an equivalent request as above:

    ```
    #SBATCH --job-name=hello_world
    #SBATCH --account=your_group
    #SBATCH --partition=standard
    #SBATCH --nodes=1
    #SBATCH --ntasks=1
    #SBATCH --mem=50gb
    #SBATCH --time=01:00:00
    ```

    On Puma, up to 94 CPUs or 470gb of memory can be requested. If using the ```mem``` flag, be sure to calculate the number of CPUs you are requesting by referring to the table with standard memory per CPU available and computing (total memory)/(memory per CPU). 

=== "Single GPU Node"

    ```
    #SBATCH --job-name=hello_world
    #SBATCH --account=your_group
    #SBATCH --partition=standard
    #SBATCH --nodes=1
    #SBATCH --ntasks=10
    #SBATCH --time=01:00:00
    #SBATCH --gres=gpu:1
    ```

    Note the ```gres=gpu:1``` option.

=== "Multi-Node"
    
    When requesting a multi-node job, up to 94 ```ntasks-per-node``` and up to ```nodes``` $\times$ ```ntasks-per-node``` total ```ntasks``` can be requested. The numbers below are chosen for illustrative purposes and can be replaced with your choice, up to system limitations.

    ```
    #SBATCH --job-name=Multi-Node-MPI-Job
    #SBATCH --account=your_group
    #SBATCH --partition=standard
    #SBATCH --ntasks=30
    #SBATCH --nodes=3
    #SBATCH --ntasks-per-node=10
    #SBATCH --time=01:00:00   
    ```

=== "High-Memory Node"
    
    When requesting a high memory node, include **both** the ```mem-per-cpu``` and ```constraint``` directives.

    ```
    #SBATCH --job-name=High-Mem-Job
    #SBATCH --account=your_group
    #SBATCH --partition=standard
    #SBATCH --nodes=1
    #SBATCH --ntasks=94
    #SBATCH --mem-per-cpu=32gb
    #SBATCH --constraint=hi_mem
    #SBATCH --time=01:00:00   
    ```