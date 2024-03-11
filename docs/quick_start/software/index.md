<link rel="stylesheet" href="../../assets/stylesheets/buttons.css">
# Software on HPC

## Accessing Software
It's hard to perform analyses without software. We learned that software packages are not available on the login nodes, but now that we're connected to a compute node, we can see and use what's available. 

Software on HPC comes [installed as modules](../../software/modules/). Modules make it easy to load and unload software from your environment. This allows hundreds of packages to be available on the same system without dependency or versioning conflicts. It's always good practice to specify which version of the software you need when loading to ensure a stable environment.

You can view and load software modules using the commands ```module avail``` and ```module load```, respectively. For example:

```
[netid@gpu66 ~]$ module avail python
 
------------------------------------------------- /opt/ohpc/pub/modulefiles --------------------------------------------------
   python/3.6/3.6.5    python/3.8/3.8.2 (D)    python/3.8/3.8.12    python/3.9/3.9.10
 
[netid@gpu66 ~]$ module load python/3.9
[netid@gpu66 ~]$ python3 --version
Python 3.9.10
```

Try running ```module avail``` without specifying any arguments. You'll notice we have *a lot* available.

## Summary

That's it! You now should have a sense of how UArizona's HPC systems are laid out, how to log in, and how to access compute nodes and software.

To continue learning about HPC, our online documentation has a lot more information that can help get you started. For example [FAQs](../../support_and_training/faqs/account_access/), information on [HPC storage](../../storage_and_transfers/storage/hpc_storage/), and [file transfers](../../storage_and_transfers/transfers/overview/). You can also find additional example batch jobs in our [Running Jobs](../../running_jobs/batch_jobs/example_batch_jobs/) section.

Other great resources include: [virtual office hours every Wednesday](../../support_and_training/consulting_services/#office-hours) from 2:00-4:00pm, consultation services offered through ServiceNow, an examples Github page with sample jobs, and a YouTube channel with training videos. 


<html>
<div class="button-container">
    <a href="../interactive_jobs"><button class="left-button"></button></a>
</div>
</html>