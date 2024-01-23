# rsync

## Overview

rsync is a fast and extraordinarily versatile file copying tool. It synchronizes files and directories between two different locations (or servers). Rsync copies only the differences of files that have actually changed. An important feature of rsync not found in most similar programs/protocols is that the mirroring takes place with only one transmission in each direction. Rsync can copy or display directory contents and copy files, optionally using compression and recursion. You use rsync in the same way you use scp. You must specify a source and a destination, one of which may be remote. 

## Example 1

Recursively transfers all files from the directory ```src/directory-name``` on the machine ```computer-name``` into the ```/data/tmp/directory-name``` directory on the local machine. The files are transferred in archive mode, which ensures that symbolic  links, devices, attributes, permissions, ownerships, etc. are preserved in the transfer. Additionally, compression will be used to reduce the size of data portions of the transfer. 

```bash
rsync -avz  computer-name:src/directory-name  user@remote.host:/data/tmp --log-file=hpc-user-rsync.log  
```

### Example 2

A trailing slash on the source changes the behavior slightly. This inclusion avoids creating an additional directory level at the destination. You can think of a trailing / on a source as meaning “copy the contents of this directory” as opposed to “copy the directory by name”, but in both cases the attributes of the containing directory are transferred to the containing directory on the destination. 

```bash
rsync -avz  computer-name:src/directory-name/  user@remote.host:/data/tmp --log-file=hpc-user-rsync.log 
```

### Additional Options

|Flag|Meaning|
|-|-|
|```-a```|Archive mode; will preserve time stamps|
|```-v```|Increase verbosity|
|```-z```|Compress file data during the transfer|
|```--log-file=FILE```|Log everything done in specified ```FILE```|