# Unsupported Software

Unfortunately, our HPC system is not configured to support all software use cases. We have summarized the main scenarios which cause software to be unsupported by our system below. Please double check that your installation requests do not meet these criteria before submitting. While the HPC may not be able to support these cases, it may be possible that other campus resources are able to. We encourage you to contact services listed in our Community Resources page to enquire about your needs.

The below list is not exhaustive and may be expanded as new scenarios are encountered. If you are unsure whether your desired software is supported, feel free to open a ticket via [ServiceNow](https://uarizona.service-now.com/sp?id=sc_cat_item&sys_id=2983102adbd23c109627d90d689619c6&sysparm_category=84d3d1acdbc8f4109627d90d6896191f) or email [hpc-consult@list.arizona.edu](mailto:hpc-consult@list.arizona.edu). 

## External Connections

Software requiring external communications that utilize protocols other than SSH are not supported. 

**Examples**

- Schrodinger remote job submitter

## Job Management/Scheduling

The UA HPC uses Slurm as its task scheduler and resource manager. Software requiring different a scheduler is therefore unsupported. 

**Examples**

- Apache Spark
- Sun Grid Engine

## Persistent Databases/Servers

The UA HPC is not configured to support databases, server instances, or other persistent software-specific daemons. 

**Examples**

- Persistent SQL databases
- Application deployments
- SAS server
