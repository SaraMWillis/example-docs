# HPC Storage Summary Overview

The University’s Research Data Center provides data storage for active analysis on the high-performance computers (HPCs). Using central computing storage services and resources, University researchers, faculty researchers, and post-doctoral researchers are able to:

* Share research data in a collaborative environment with other UArizona affiliates on the HPC system
* Store large-scale computational research data
* Request additional storage for further data analysis

The storage is mounted as a filesystem and all the clusters have access to the same filesystems.

Every user has access to individual and shared storage on the system where they can host data for active analyses. A summary of these locations is shown below:

|<div style="width:120px">Path</div>|Description|<div style="width:120px">Quota</div>|Duration|
|-|-|-|-|
|```/home/uxx/netid```|An individual storage allocation provided for every HPC user|50gb|Accessible for the duration of user's account|
|```/groups/pi_netid```|A communal storage allocation provided for every research group|500gb|Accessible for the duration of a PI's account|
|```/xdisk/pi_netid```|Temporary communal storage available for every group on request. See xdisk section below for details.|200gb-20tb|Up to 300 days|
|```/tmp```|Local storage available on individual compute nodes.|$<$ 800GB to 1.4TB|Only accessible for the duration of a job's run.|