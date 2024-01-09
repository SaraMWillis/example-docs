# General Computing

??? question "Why aren't common commands working?"
    There may be a few reasons for this. First, make sure your shell is set to Bash. If your shell is not set to Bash, contact our consultants so that they can reset it for you.
    
    If your shell is set to bash, double-check that you haven't changed, overwritten, or aliased anything important either your ~/.bashrc or ~/.bash_profile. E.g., unsetting your ```PATH```, aliasing ```.```, and so on will corrupt your environment and prevent you from interacting with HPC normally. 

??? question "Why is my terminal glitching (e.g. ++ctrl+a++ puts me in the middle of my command prompt)?"
    When you log into HPC, the variable ```$COMMAND_PROMPT``` is set to display your current cluster (e.g. ```(puma)```). Sometimes this can cause formatting problems. If you'd prefer to modify your ```$PS1``` (command prompt variable) instead, you can add the following to your ```~/.bashrc```:
    ```bash
    if [ -n "${PROMPT_COMMAND}" -a -r /usr/local/bin/slurm-selector.sh ]; then
    SavePS1=${PS1}
    Cur_Cluster=$(eval ${PROMPT_COMMAND} 2>/dev/null)
    PS1="${Cur_Cluster}${SavePS1}"
    unset PROMPT_COMMAND
    for c in puma ocelote elgato; do
        alias ${c}="PS1=\"(${c}) ${SavePS1}\"; . /usr/local/bin/slurm-selector.sh ${c}; unset PROMPT_COMMAND"
    done
    unset Cur_Cluster SavePS1
    fi
    ```

??? question "What are dot files and what is a ```~/.bashrc```?"
    Files that start with a dot, i.e. a ```.```, are hidden when executing ```ls``` without additional options. If you use ```ls -la```, that will show you all the files that exist, both standard and hidden. Dot files are generally important configuration files so it's important to be careful with their contents and deleting them. 

    Your bashrc is a specific dot file that lives in your home directory (```~``` is just shorthand for your home) and defines your environment every time you log in. Any commands you add to that file will be run whenever you access the system. This means, if you have common aliases you like to use, paths you like exported in your environment, etc., these can be added to your bashrc to avoid the headache of having to define them in every session.

    A word of caution. Be careful with the contents of this file. Some things to avoid:

    Don't alias important Linux commands. For example, the character ```.``` is a shortcut for source. If you do something like add alias ```.="echo foo"``` to your bashrc, you will lose basic functionality in the terminal, e.g., access to modules, virtual environments, etc. 
    
    Do not recursively source your configuration files. For example, if you add ```source ~/.bashrc``` or source ```~/.bash_profile``` to your bashrc, then you will enter an infinite sourcing loop. This means, if you try to log in, your terminal will freeze for a moment before your access is denied. 
    Be careful with echoes. If you use CLI tools for data transfer, e.g. ```scp``` or ```sftp```, they may require a "silent" terminal. If you're trying to initiate transfers and are getting the error "Received message too long", check your bashrc to make sure you aren't printing anything to the terminal. 