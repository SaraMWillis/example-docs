# SSH Keys
## Why Use SSH Keys?

The Bastion Host uses two-factor authentication and will, by default, prompt you for a password and 2nd factor when you attempt to log in. As an alternative, you can use PKI (Public Key Authentication). This means you will not have to provide a password or Duo-authenticate for any future sessions. To do this, you will need to create an SSH Key on your local workstation and copy the public key to the ```~/.ssh/authorized_keys``` file in your HPC account on the bastion host.

## Create and Use SSH Keys


=== "Linux/Mac"
    In a Terminal session on your local workstation:

    1. Create a public-key pair: 
    ```bash
    $ ssh-keygen -t rsa
    ```
    You will be prompted to enter a passphrase. This is optional, but we strongly recommend that you do so.
        
    2. After running that command, you will have two new files on your local computer: ```~/.ssh/id_rsa``` and ```~/.ssh/id_rsa.pub```
        ```id_rsa``` is your private key file. Do not share this with anybody! It is analagous to your password; anybody who has this file can impersonate you.
        ```id_rsa.pub``` is your public key file. You will upload this onto any servers that you wish to automatically login to.
        
    3. Copy the public key to the Bastion Host (you will need to enter your password this one time): 
    ```bash
    $ ssh-copy-id netid@hpc.arizona.edu
    ```
    3b. If your computer does not support the ssh-copy-id command, run the following commands:
    ```bash
    $ scp ~/.ssh/id_rsa.pub netid@hpc.arizona.edu:
    $ ssh netid@hpc.arizona.edu # (you will need to use your password this time)
    $ mkdir -p ~/.ssh && cat ~/id_rsa.pub >> .ssh/authorized_keys && rm ~/id_rsa.pub # On the server, copies the key into the appropriate file
    ```
        
    Now, logout and attempt to login to the server again. You should not be prompted for a password!
        
=== "Windows"
    To setup SSH keys on Windows with the PuTTy client, refer to the [official PuTTy documentation](http://the.earth.li/~sgtatham/putty/0.63/htmldoc/Chapter8.html#pubkey).

## Using SSH Keys for file transfers

Note that SSH Keys can also be used to avoid entering a password and 2nd factor when transferring files to to the cluster via the file transfer node (```filexfer.hpc.arizona.edu```) using command line programs like ```scp``` or ```sftp```.  Follow the steps above (2-4 under the Mac and Linux instructions), except use ```filexfer.hpc.arizona.edu``` instead of ```hpc.arizona.edu```. Note that you only need to generate the keys in Step 1 once. The same ```~/.ssh/id_rsa.pub``` file may be used to identify yourself to multiple hosts.