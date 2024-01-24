# Rental Storage

<link rel="stylesheet" href="../../../../overrides/animated_dropdown.css">
<link rel="stylesheet" href="../../../../overrides/spacing.css">

<html>

<!-- General format for HTML 
<button class="collapsible">Question goes here</button>
<div class="content">
  <p>
      Answer goes here
  </p>
</div>
-->

<!-- How do I request rental storage? -->
<button class="collapsible">How do I request rental storage?</button>
<div class="content">
  <p>
       Rental storage can be requested by PIs through the <a href="https://portal.hpc.arizona.edu/portal/">user portal</a>. A guide with screenshots can found in our <a href="../../../../storage_and_transfers/storage/rental_storage/">rental storage documentation</a>. 
  </p>
</div>

<!-- Why can't I see my rental allocation when I log into HPC? --> 
<button class="collapsible">Why can't I see my rental allocation when I log into HPC?</button>
<div class="content">
  <p>
      Rental allocations are not mounted on the login or compute nodes. You can access your allocation by logging in to our data transfer nodes: <code>filexfer.hpc.arizona.edu</code>
  </p>
</div>

<!-- Can I analyze data stored in /rental directly in my jobs? -->
<button class="collapsible">Can I analyze data stored in /rental directly in my jobs?</button>
<div class="content">
  <p>
      No, rental storage is not mounted on the HPC login or compute nodes which means jobs cannot access <code>/rental</code> directly. Data stored in <code>/rental</code> need to be moved to <code>/home</code>, <code>/groups</code>, or <code>/xdisk</code> to be available. 
  </p>
</div>


<div class="vertical-space"></div>
<script src="../../../../overrides/animated_dropdown.js"></script>
</html>