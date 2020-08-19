---


---

<p>First, SSH remote into your EC2 instance using Putty and add the Apache2 system packages below, type command:</p>
<pre><code>sudo add-apt-repository ppa:ondrej/apache2
</code></pre>
<p>Then press  <code>Enter</code>  on the screen to continue.</p>
<p>Update the packages currently installed on the system, type command:</p>
<pre><code>sudo apt update
</code></pre>
<p>Now install Apache2 Web Server, type command:</p>
<pre><code>sudo apt-get install apache2 -y
</code></pre>
<p>After installation completed, verify the Apache2 version.</p>
<pre><code>sudo apache2ctl -v
</code></pre>
<p>The output looks like this:</p>
<pre><code>Server version: Apache/2.4.41 (Ubuntu)
Server built:   2019-04-02T20:30:26```
</code></pre>

