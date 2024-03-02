# iRods

!!! tip
    If you are looking for information on how to connect to CyVerse's data store, [see their iRODS documentation for a guide](https://learning.cyverse.org/ds/icommands/#icommands-first-time-configuration).

iRODS 4 is installed as a standard package to the operating system on every node. This means you will not have to "module load irods". You will still need to ```iinit``` the first time (see below). iRODS is also available on the filexfer nodes for use.

## Initializing iRODS

Running ```iinit``` for any system using iRODS 4.x, unlike its iRODS3 counterpart, does not help you set up the environment. Instead, you need to run ```create_irods_env``` with suitable options for the iRODS host, zone, username,etc manually.

|For this key|Enter this|
|-|-|
|```-h```| <hostname of iRODS server>|
|```-p```|<port number of iRODS server> (1247 is default)|
|```-z```|<Zone name of iRODS zone>|
|```-u```|<user name on the iRODS server> (may not match your netid)|
|```-a```|<authentication method for the iRODS server> (PAM, native,...)|

For example
```
$ create_irods_env -a native -h someserver.somewhere.net -z MYZONE
```

will suffice to create an appropriate ```~/.irods/irods_environment.json``` file to allow you to run ```iinit```; we took the default ```-p 1247```, ```-u <your NetId>``` in the above example by omitting ```-p``` and ```-u```.  You only need to do this step ONE time; subsequent times you will just run iinit and it will asked for your password. Note ```create_irods_env``` will NOT overwrite or alter an existing ```~/.irods/irods_environment.json``` file.

Once the  ```~/.irods/irods_environment.json``` file is created properly, you should be able to sign in to the iRods server your selected using ```iinit```, viz:

```
$ iinit
Enter your current ... password:    # enter your iRODS server password here
```

At this point you can use other iRods commands such as ```icp``` to move files.

## Examples
!!! tip
    In the following examples:
    * ```my-files-to-transfer/``` is the example name of the directory or folder for bulk transfers.
    * ```my-file-to-transfer.txt``` is the example name for single file transfers.
    * Any filename may be used for the ```checkpoint-file```.

**Bulk Files Transfer Example**
```
iput -P -b -r -T --retries 3 -X checkpoint-file my-files-to-transfer/
```

**Single Large File Transfer Example**
```
iput -P -T --retries 3 --lfrestart checkpoint-lf-file my-file-to-transfer.txt
```