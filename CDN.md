---


---

<h1 id="distribute-website-via-cloudfront">Distribute Website via CloudFront</h1>
<ol>
<li>Select “Services” from the top left corner and enter “cloud front” in the “Find a service by name or feature” text box and select “CloudFront”.</li>
</ol>
<p><a href="https://classroom.udacity.com/nanodegrees/nd9990/parts/4bf365d7-4a50-4fc0-aee3-30ad1e60c15d/modules/1cf10ed1-e953-4911-8d27-982d6ae97ae1/lessons/cc6eb870-02d0-4825-8fae-b552bd531c7c/concepts/e5301d44-0c4f-4ff6-9790-a0406ff65e9a#"></a></p>
<p><img src="https://video.udacity-data.com/topher/2019/May/5cee95b3_screen-shot-2019-05-18-at-12.22.56-pm/screen-shot-2019-05-18-at-12.22.56-pm.png" alt=""></p>
<ol start="2">
<li>From the CloudFront dashboard, click “Create Distribution”.</li>
</ol>
<p><a href="https://classroom.udacity.com/nanodegrees/nd9990/parts/4bf365d7-4a50-4fc0-aee3-30ad1e60c15d/modules/1cf10ed1-e953-4911-8d27-982d6ae97ae1/lessons/cc6eb870-02d0-4825-8fae-b552bd531c7c/concepts/e5301d44-0c4f-4ff6-9790-a0406ff65e9a#"></a></p>
<p><img src="https://video.udacity-data.com/topher/2019/May/5cee95b1_screen-shot-2019-05-18-at-12.24.43-pm/screen-shot-2019-05-18-at-12.24.43-pm.png" alt=""></p>
<ol start="3">
<li>For “Select a delivery method for your content”, click “Get Started”.</li>
</ol>
<p><a href="https://classroom.udacity.com/nanodegrees/nd9990/parts/4bf365d7-4a50-4fc0-aee3-30ad1e60c15d/modules/1cf10ed1-e953-4911-8d27-982d6ae97ae1/lessons/cc6eb870-02d0-4825-8fae-b552bd531c7c/concepts/e5301d44-0c4f-4ff6-9790-a0406ff65e9a#"></a></p>
<p><img src="https://video.udacity-data.com/topher/2019/May/5cee95ab_screen-shot-2019-05-18-at-1.08.32-pm/screen-shot-2019-05-18-at-1.08.32-pm.png" alt=""></p>
<ol start="4">
<li>Under “Origin Settings”:
<ul>
<li>Under “Origin Domain Name”, select the S3 bucket that you just created.</li>
<li>Under “Origin Path”, enter “/” to indicate the root level.</li>
</ul>
</li>
</ol>
<p><a href="https://classroom.udacity.com/nanodegrees/nd9990/parts/4bf365d7-4a50-4fc0-aee3-30ad1e60c15d/modules/1cf10ed1-e953-4911-8d27-982d6ae97ae1/lessons/cc6eb870-02d0-4825-8fae-b552bd531c7c/concepts/e5301d44-0c4f-4ff6-9790-a0406ff65e9a#"></a></p>
<p><img src="https://video.udacity-data.com/topher/2019/May/5cee95af_screen-shot-2019-05-18-at-1.07.44-pm/screen-shot-2019-05-18-at-1.07.44-pm.png" alt=""></p>
<ol start="5">
<li>Leave the defaults for the rest of the options, scroll down, and click “Create Distribution”.</li>
</ol>
<p><strong><em>Note:</em></strong>  It may take up to  <strong><em>10 minutes</em></strong>  for the CloudFront Distribution to be created.</p>
<ol start="6">
<li>Once the status of your distribution changes from “In Progress” to “Deployed”, copy the endpoint URL for your CloudFront distribution found in the “Domain Name” column.</li>
</ol>
<p><a href="https://classroom.udacity.com/nanodegrees/nd9990/parts/4bf365d7-4a50-4fc0-aee3-30ad1e60c15d/modules/1cf10ed1-e953-4911-8d27-982d6ae97ae1/lessons/cc6eb870-02d0-4825-8fae-b552bd531c7c/concepts/e5301d44-0c4f-4ff6-9790-a0406ff65e9a#"></a></p>
<p><img src="https://video.udacity-data.com/topher/2019/May/5cee95a9_screen-shot-2019-05-18-at-12.40.31-pm/screen-shot-2019-05-18-at-12.40.31-pm.png" alt=""></p>
<p>In this example, the Domain Name value is  <code>d34jyue2fsjani.cloudfront.net</code>, but  <strong><em>yours will be different.</em></strong></p>

