# Rclone

Rclone is a CLI installed on ```filexfer.hpc.arizona.edu``` that can be used to transfer files to Google Drive as well as other Cloud-based storage sites. To use rclone, you will need to start by configuring it. The walkthrough provided by rclone is fairly straightforward. 

For information on rclone commands, see: [https://rclone.org/commands/](https://rclone.org/commands/)

=== "Google Drive"
    ```
    [netid@sdmz-dtn-4 ~]$ rclone config
    Name                 Type
    ====                 ====
 
    e) Edit existing remote
    n) New remote
    d) Delete remote
    r) Rename remote
    c) Copy remote
    s) Set configuration password
    q) Quit config
    e/n/d/r/c/s/q> n
    name> GoogleDrive
    Type of storage to configure.
    Enter a string value. Press Enter for the default ("").
    Choose a number from below, or type in your own value
    ...
    12 / Google Drive
       \ "drive"
    ...
    Storage> 12
    Google Application Client Id
    client_id>
    client_secret>
    scope> 1
    root_folder_id>
    service_account_file>
    Edit advanced config? (y/n)
    y) Yes
    n) No
    y/n> n

    The next prompt will ask if you would like to use auto config, select N here or the configuration will not be successful. You will be given a URL. Copy and paste this into your web browser and follow the prompts to allow rclone to have access to your UArizona Google Drive account. When you are done, it will give you a verification code. Copy and paste this back into the terminal to proceed.

    Remote config
    Use auto config?
      * Say Y if not sure
      * Say N if you are working on a remote or headless machine
    y) Yes
    n) No
    y/n> N
    If your browser doesn't open automatically go to the following link: <long URL>
    Log in and authorize rclone for access
    Enter verification code> <your verification code here>
    Configure this as a team drive?
    y) Yes
    n) No
    y/n> n
    --------------------
    [GoogleDrive]
    type = drive
    scope = drive
    token = {"access_token": <lots of token data>}
    --------------------
    y) Yes this is OK
    e) Edit this remote
    d) Delete this remote
    y/e/d> y
    Current remotes:
 
    Name                 Type
    ====                 ====
    GoogleDrive          drive

    Your Google Drive connection is now active and you can use rclone to make transfers. 
    ```

=== "AWS Tier 2"
    ```
    [netid@sdmz-dtn-4 ~]$ rclone config
    Current remotes:
 
    Name                 Type
    ====                 ====
 
    e) Edit existing remote
    n) New remote
    d) Delete remote
    r) Rename remote
    c) Copy remote
    s) Set configuration password
    q) Quit config
    e/n/d/r/c/s/q> n
    name> AWS
    Storage> s3
    provider> AWS
    env_auth> false
    access_key_id> YOUR_KEY_ID_HERE
    secret_access_key> YOUR_SECRET_ACCESS_KEY_HERE
    region> us-west-2
    endpoint>
    location_constraint>
    acl>
    server_side_encryption>
    sse_kms_key_id>
    storage_class> INTELLIGENT_TIERING
    Edit advanced config? (y/n)
    y) Yes
    n) No
    y/n> n
    ```