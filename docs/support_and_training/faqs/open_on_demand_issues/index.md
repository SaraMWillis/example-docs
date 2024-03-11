# Open OnDemand Issues


<link rel="stylesheet" href="../../../assets/stylesheets/animated_dropdown.css">
<link rel="stylesheet" href="../../../assets/stylesheets/spacing.css">


<html>
    
<button class="collapsible">Why am I getting a message saying I'm not sponsored when trying to log in?</button>
<div class="content">
  <p>
      If you are trying to log in to Open Ondemand and are seeing the following:
      <img src="images/not_yet_approved.png" style="width:500px;">
      <ul>
          <li>You have not yet been sponsored by a faculty member. See our Account Creation page for instructions on getting registered for HPC.</li>
          <li>If you are already registered for HPC, this may be a browser issue. Try logging in again in an incognito session or different browser to test. If this succeeds, clearing your browser's cookies should help.</li>
      </ul>
  </p>
</div>

<button class="collapsible">Why am I getting a "Bad Request" message when trying to connect?</button>
<div class="content">
  <p>
      If you are trying to log in to Open Ondemand and are seeing the following:
      <br>
      <img src="images/bad_request.png" style="width:500px;">
      <br>
      this may be a browser issue. Try logging in again in an incognito session or different browser to test. If this succeeds, clearing your browser's cache should help.
  </p>
</div>

<button class="collapsible">Why am I getting an error saying "We're sorry, but something went wrong" when trying to log in?</button>
<div class="content">
  <p>
      If you are trying to log in to Open Ondemand and are seeing the following:
      <br>
      <img src="images/somethingwentwrong.png" style="width:500px;">
      <br>
      check your storage usage in your home directory. You can do this by logging into HPC in a terminal session and using the command uquota. If your storage usage is >50GB, OnDemand cannot create the temporary files necessary to give access to the website. Try clearing out some space in your home and then logging back into OnDemand.
  </p>
</div>

<button class="collapsible">Why are my Desktop sessions failing with 'Could not connect to session bus: failed to connect to socket /tmp/dbus-'?</button>
<div class="content">
  <p>
      If you're seeing:
      <br>
      <img src="images/dbus_error.png" style="width:500px;">
      <br>
      when trying to connect to an interactive desktop session, the likely culprit is Anaconda. For a permanent solution, you can run the following command from an interactive terminal session:
      <pre><code>
conda config --set auto_activate_base false
      </code></pre>
      This will prevent conda from auto-activating when you first log in and allow you to have more control over your environment. When you'd like to activate anaconda, run conda activate. See this example for information running anaconda workflows in batch with auto-activation disabled.
  </p>
</div>
    
    
<div class="vertical-space"></div>
<script src="../../../assets/javascripts/animated_dropdown.js"></script>


</html>
