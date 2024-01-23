# General Computing

<link rel="stylesheet" href="../../../overrides/animated_dropdown.css">
<link rel="stylesheet" href="../../../overrides/prism.css">
<link rel="stylesheet" href="../../../overrides/spacing.css">

<html>

<button class="collapsible">Why aren't common commands working?</button>
<div class="content">
  <p>There may be a few reasons for this. First, make sure your shell is set to Bash. If your shell is not set to Bash, contact our consultants so that they can reset it for you.
  <br>
  If your shell is set to bash, double-check that you haven't changed, overwritten, or aliased anything important either your <code>~/.bashrc</code> or <code>~/.bash_profile</code>. E.g., unsetting your <code>PATH</code>, aliasing <code>.</code>, and so on will corrupt your environment and prevent you from interacting with HPC normally. 
  </p>
</div>

<button class="collapsible">Why is my terminal glitching (e.g. <kbd>Ctrl</kbd>+<kbd>a</kbd> puts me in the middle of my command prompt)?</button>
<div class="content">
  <p>When you log into HPC, the variable <code>$COMMAND_PROMPT</code> is set to display your current cluster (e.g. <code>(puma)</code>). Sometimes this can cause formatting problems. If you'd prefer to modify your <code>$PS1</code> (command prompt variable) instead, you can add the following to your <code>~/.bashrc</code>:
  <br>
  <pre><code class="language-bash">if [ -n "${PROMPT_COMMAND}" -a -r /usr/local/bin/slurm-selector.sh ]; then
  SavePS1=${PS1}
  Cur_Cluster=$(eval ${PROMPT_COMMAND} 2>/dev/null)
  PS1="${Cur_Cluster}${SavePS1}"
  unset PROMPT_COMMAND
  for c in puma ocelote elgato; do
    alias ${c}="PS1=\"(${c}) ${SavePS1}\"; . /usr/local/bin/slurm-selector.sh ${c}; unset PROMPT_COMMAND"
  done
  unset Cur_Cluster SavePS1
fi
  </code></pre>
  </p>
</div>

<button class="collapsible">What are dot files and what is a <code>~/.bashrc</code>?</button>
<div class="content">
  <p>Files that start with a dot, i.e. a <code>.</code>, are hidden when executing <code>ls</code> without additional options. If you use <code>ls -la</code>, that will show you all the files that exist, both standard and hidden. Dot files are generally important configuration files so it's important to be careful with their contents and deleting them. 
  <br>
  Your bashrc is a specific dot file that lives in your home directory (<code>~</code> is just shorthand for your home) and defines your environment every time you log in. Any commands you add to that file will be run whenever you access the system. This means, if you have common aliases you like to use, paths you like exported in your environment, etc., these can be added to your bashrc to avoid the headache of having to define them in every session.
  <br>
  <b>A word of caution.</b> Be careful with the contents of this file. Some things to avoid:
  <br><br>
    &ensp;1. Don't alias important Linux commands. For example, the character <code>.</code> is a shortcut for source. If you do something like add alias <code>.="echo foo"</code> to your bashrc, you will lose basic functionality in the terminal, e.g., access to modules, virtual environments, etc. 
    <br>
    &ensp;2. Do not recursively source your configuration files. For example, if you add <code>source ~/.bashrc</code> or <code>source ~/.bash_profile</code> to your bashrc, then you will enter an infinite sourcing loop. This means when you try to log in, your terminal will freeze for a moment before your access is denied. 
    <br>
    &ensp;3. Be careful with echoes. If you use CLI tools for data transfer, e.g. <code>scp</code> or <code>sftp</code>, they may require a "silent" terminal. If you're trying to initiate transfers and are getting the error "Received message too long", check your bashrc to make sure you aren't printing anything to the terminal. 
  </p>
</div>

<div class="vertical-space"></div>
<script src="../../../overrides/animated_dropdown.js"></script>
<script src="../../../overrides/prism.js"></script>

</html>