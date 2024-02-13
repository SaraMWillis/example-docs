# Tier 2 AWS Storage

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

<!-- Who can submit a Tier 2 storage request? -->
<button class="collapsible">Who can submit a Tier 2 storage request?</button>
<div class="content">
  <p>
    A PI must submit their group's storage request. The exception to this is if a group member has been <a href="../../../registration_and_access/group_management/delegating_group_management_rights/">designated xdisk/storage delegate</a>. Delegates may submit a request on behalf of their PI by switching users in the user portal.
  </p>
</div>

<!-- How long is the turnaround time to between submitting the storage request and obtaining an S3 account? -->
<button class="collapsible">How long is the turnaround time to between submitting the storage request and obtaining an S3 account?</button>
<div class="content">
  <p>
     In most cases it will be in one business day.
  </p>
</div>

<!-- Can I move my data directly from Google Drive to the new S3 account? -->
<button class="collapsible">Can I move my data directly from Google Drive to the new S3 account?</button>
<div class="content">
  <p>
     Yes. Using <a href="../../../storage_and_transfers/transfers/globus/">Globus</a> you can move data from Google Drive to S3.
  </p>
</div>

<!-- What is the pricing for S3? -->
<button class="collapsible">Question goes here</button>
<div class="content">
  <p>
    You should check <a href="https://aws.amazon.com/s3/pricing/?nc=sn&loc=4">the Amazon site</a>. As of March 2022:
    <ul>
        <li>Frequent Access Tier, First 50 TB / Month $0.023 per GB</li>
        <li>Frequent Access Tier, Next 450 TB / Month $0.022 per GB</li>
        <li>Frequent Access Tier, Over 500 TB / Month $0.021 per GB</li>
    </ul>
  </p>
</div>

<!-- Can I move my data directly to Glacier if I know it is archival. That way I can skip the S3 expenses? -->
<button class="collapsible">Can I move my data directly to Glacier if I know it is archival. That way I can skip the S3 expenses?</button>
<div class="content">
  <p>
    Not in the first release, but potentially as a future offering.
  </p>
</div>

<!-- Is the monthly billing based on average usage? -->
<button class="collapsible">Is the monthly billing based on average usage?</button>
<div class="content">
  <p>
     Yes. The capacity used is recorded daily and the billing is a monthly average.
  </p>
</div>

<!-- What is a KFS number? -->
<button class="collapsible">What is a KFS number?</button>
<div class="content">
  <p>
     It is used for accounting purposes and used by your Department's finance specialist.
  </p>
</div>

<!-- Can I view my storage in each of S3, Glacier and Deep Glacier? -->
<button class="collapsible">Can I view my storage in each of S3, Glacier and Deep Glacier?</button>
<div class="content">
  <p>
     Yes, you can use the CLI (command line interface) for information about your usage
  </p>
</div>

<!-- Can I limit the amount of data that goes into S3 so I can control the expense? -->
<button class="collapsible">Can I limit the amount of data that goes into S3 so I can control the expense?</button>
<div class="content">
  <p>
     No, but you can track the usage and remove any data that should not be there.
  </p>
</div>

<!-- What is the difference between Glacier and Deep Glacier? -->
<button class="collapsible">What is the difference between Glacier and Deep Glacier?</button>
<div class="content">
  <p>
     Glacier is effectively large, slow disks and Deep Glacier is tape storage.
  </p>
</div>

<!-- I use workflows to move data using google drive, and to share with others. Will AWS support something similar? -->
<button class="collapsible">I use workflows to move data using google drive, and to share with others. Will AWS support something similar?</button>
<div class="content">
  <p>
     Amazon S3 will likely support what you do. Perhaps our consultants can help to rework your workflows.
  </p>
</div>

<!-- Are there charges for data movement? -->
<button class="collapsible">Are there charges for data movement?</button>
<div class="content">
  <p>
     You will not be charged for data ingress, egress or other operations.
  </p>
</div>

<!-- Can I have multiple S3 buckets associated with my account? -->
<button class="collapsible">Can I have multiple S3 buckets associated with my account?</button>
<div class="content">
  <p>
    Yes
  </p>
</div>

<!-- Are there any limits on uploads, e.g. may transfer size / day? -->
<button class="collapsible">Are there any limits on uploads, e.g. may transfer size/day?</button>
<div class="content">
  <p>
    The max file size is 5TB based on <a href="https://docs.aws.amazon.com/AmazonS3/latest/userguide/qfacts.html">Amazon's official documentation</a>.
  </p>
</div>

<!-- What why am I receiving an email: "ALARM: "ua-rt-t2-netid capacity growth alarm" in US West (Oregon)"?  -->
<button class="collapsible">What why am I receiving an email: "ALARM: "ua-rt-t2-netid capacity growth alarm" in US West (Oregon)"?</button>
<div class="content">
  <p>
    This alert is sent to notify you whenever your storage usage grows by 10% relative to the previous week. This ensures that you're aware of any unintended spikes and the potential resulting costs. 
  </p>
</div>




<div class="vertical-space"></div>
<script src="../../../../overrides/animated_dropdown.js"></script>
</html>