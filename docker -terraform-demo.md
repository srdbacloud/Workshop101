


---

<ol>
<li>
<p><strong>Pre-requisite</strong></p>
<ol>
<li>Create an EC2 –  <a href="https://acloudxpert.com/creating-a-linux-based-ec2-instance/">Please refer this link</a></li>
<li>Install Docker –  <a href="https://acloudxpert.com/how-toinstall-docker-on-amazon-linux-ami/">Please refer this link</a></li>
<li>Install Terraform –  <a href="https://acloudxpert.com/how-to-install-terraform-on-amazon-linux-ami-ec2/">Please refer this link</a></li>
</ol>
</li>
<li>
<p><strong>Terraform Commands:</strong></p>
<ol>
<li>
<p>List the Terraform commands:<br>
<code>terraform</code><br>
Common commands:<br>
<code>apply</code>: Builds or changes infrastructure<br>
<code>console</code>: Interactive console for Terraform interpolations<br>
<code>destroy</code>: Destroys Terraform-managed infrastructure<br>
<code>fmt</code>: Rewrites configuration files to canonical format<br>
<code>get</code>: Downloads and installs modules for the configuration<br>
<code>graph</code>: Creates a visual graph of Terraform resources<br>
<code>import</code>: Imports existing infrastructure into Terraform<br>
<code>init</code>: Initializes a new or existing Terraform configuration<br>
<code>output</code>: Reads an output from a state file<br>
<code>plan</code>: Generates and shows an execution plan<br>
<code>providers</code>: Prints a tree of the providers used in the configuration<br>
<code>push</code>: Uploads this Terraform module to Terraform Enterprise to run<br>
<code>refresh</code>: Updates local state file against real resources<br>
<code>show</code>: Inspects Terraform state or plan<br>
<code>taint</code>: Manually marks a resource for recreation<br>
<code>untaint</code>: Manually unmarks a resource as tainted<br>
<code>validate</code>: Validates the Terraform files<br>
<code>version</code>: Prints the Terraform version<br>
<code>workspace</code>: Workspace management</p>
</li>
<li>
<p>Set up the environment:</p>
<p>mkdir -p terraform/basics<br>
cd terraform/basics</p>
</li>
<li>
<p>Create a Terraform script:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><a href="http://main.tf">main.tf</a> contents:</p>
<h1 id="download-the-latest-ghost-image">Download the latest Ghost image</h1>
<p>resource “docker_image” “image_id” {<br>
name = “ghost:latest”<br>
}</p>
<h1 id="start-the-container">Start the Container</h1>
<p>resource “docker_container” “container_id” {<br>
name  = “ghost_blog”<br>
image = “${docker_image.image_id.latest}”<br>
ports {<br>
internal = “2368”<br>
external = “80”<br>
}<br>
}</p>
</li>
<li>
<p>Initialize Terraform:</p>
<p>terraform init</p>
</li>
<li>
<p>Validate the Terraform file:</p>
<p>terraform validate</p>
</li>
<li>
<p>List providers in the folder:</p>
<p>ls .terraform/plugins/linux_amd64/</p>
</li>
<li>
<p>List providers used in the configuration:</p>
<p>terraform providers</p>
</li>
<li>
<p>Terraform Plan:</p>
<p>terraform plan</p>
<p>Useful flags for  <code>plan</code>:<br>
<code>-out=path</code>: Writes a plan file to the given path. This can be used as input to the “apply” command.<br>
<code>-var 'foo=bar'</code>: Set a variable in the Terraform configuration. This flag can be set multiple times.</p>
</li>
<li>
<p>Terraform Apply:</p>
<p>terraform apply</p>
<p>Useful flags for  <code>apply</code>:<br>
<code>-auto-approve</code>: This skips interactive approval of plan before applying.<br>
<code>-var 'foo=bar'</code>: This sets a variable in the Terraform configuration. It can be set multiple times.</p>
<p>Confirm your apply by typing  <code>yes</code>. The apply will take a bit to complete.</p>
</li>
<li>
<p>List the Docker images:</p>
</li>
</ol>
<pre><code>docker image ls
</code></pre>
<ol start="11">
<li>Terraform Show:</li>
</ol>
<pre><code>terraform show
</code></pre>
<ol start="12">
<li>Terraform Destroy:</li>
</ol>
<pre><code>terraform destroy

Useful flags for destroys:  
`-auto-approve`: Skip interactive approval of plan before applying.  
Confirm your destroy by typing  `yes`.
</code></pre>
<ol start="13">
<li>Re-list the Docker images:</li>
</ol>
<pre><code>docker image ls
</code></pre>
<ol start="14">
<li>Using a plan:</li>
</ol>
<pre><code>terraform plan -out=tfplan
</code></pre>
<ol start="15">
<li>Applying a plan:</li>
</ol>
<pre><code>terraform apply tfplan
</code></pre>
<ol start="16">
<li>Show the Docker Image resource:</li>
</ol>
<pre><code>terraform show
</code></pre>
<ol start="17">
<li>Destroy the resource once again:</li>
</ol>
<pre><code>terraform destroy
</code></pre>
<ol start="18">
<li>Open Ghost blog using Docker IP</li>
</ol>
</li>
<li>
<p><strong>Tainting and Updating Resources</strong></p>
<ol>
<li>
<p>Tainting a resource:</p>
<p>terraform taint docker_container.container_id</p>
<p>Check tainted resource which will be recreated using</p>
<p>terraform plan</p>
</li>
<li>
<p>Untainting a resource:</p>
<p>terraform untaint docker_container.container_id</p>
</li>
<li>
<p>Let’s edit  <code>main.tf</code>  and change the image to  <code>ghost:alpine</code>.</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p>replace the existing content with below one</p>
<pre><code># Download the latest Ghost image
resource "docker_image" "image_id" {
  name = "ghost:alpine"
}

# Start the Container
resource "docker_container" "container_id" {
  name  = "ghost_blog"
  image = "${docker_image.image_id.latest}"
  ports {
    internal = "2368"
    external = "80"
  }
}
</code></pre>
</li>
<li>
<p>Now do a terraform validate, plan &amp; apply</p>
<p>terraform validate<br>
terraform plan<br>
terraform apply</p>
</li>
<li>
<p>Check the new image id by using</p>
<p>docker images ls</p>
</li>
<li>
<p>Reset the environment:</p>
<p>terraform destroy</p>
<p>Confirm the <code>destroy</code> by typing <strong>yes</strong>.<br>
List the Docker images:</p>
<p>docker image ls</p>
<p>Remove the Ghost blog image:</p>
<p>docker image rm ghost:latest</p>
<p>Reset <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code># Download the latest Ghost image
resource "docker_image" "image_id" {
  name = "ghost:latest"
}

# Start the Container
resource "docker_container" "container_id" {
  name  = "ghost_blog"
  image = "${docker_image.image_id.latest}"
  ports {
    internal = "2368"
    external = "80"
  }
}
</code></pre>
</li>
</ol>
</li>
<li>
<p><strong>Terraform Console and Output</strong></p>
<ol>
<li>
<p>Redeploy the Ghost image and container:</p>
<p>terraform apply</p>
</li>
<li>
<p>Show the Terraform resources:</p>
<p>terraform show</p>
</li>
<li>
<p>Start the Terraform console:</p>
<p>terraform console</p>
</li>
<li>
<p>Type the following in the console to get the container’s name:</p>
<p>docker_container.container_id.name</p>
</li>
<li>
<p>Type the following in the console to get the container’s IP:</p>
<p>docker_container.container_id.ip_address</p>
<p>Break out of the Terraform console by using <strong>Ctrl+C</strong>.</p>
</li>
<li>
<p>Destroy the environment:</p>
<p>terraform destroy</p>
</li>
<li>
<p>Edit <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code># Download the latest Ghost Image
resource "docker_image" "image_id" {
  name = "ghost:latest"
}

# Start the Container
resource "docker_container" "container_id" {
  name  = "blog"
  image = "${docker_image.image_id.latest}"
  ports {
    internal = "2368"
    external = "80"
  }
}

#Output the IP Address of the Container
output "ip_address" {
  value       = "${docker_container.container_id.ip_address}"
  description = "The IP for the container."
}

#Output the Name of the Container
output "container_name" {
  value       = "${docker_container.container_id.name}"
  description = "The name of the container."
}

</code></pre>
</li>
<li>
<p>Validate &amp; Apply changes:</p>
<p>terraform validate<br>
terraform apply</p>
</li>
<li>
<p>Reset the environment:</p>
<p>terraform destroy</p>
</li>
</ol>
</li>
<li>
<p>Input Variables</p>
<ol>
<li>
<p>Edit <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code>#Define variables
variable "image_name" {
  description = "Image for container."
  default     = "ghost:latest"
}

variable "container_name" {
  description = "Name of the container."
  default     = "blog"
}

variable "int_port" {
  description = "Internal port for container."
  default     = "2368"
}

variable "ext_port" {
  description = "External port for container."
  default     = "80"
}

# Download the latest Ghost Image
resource "docker_image" "image_id" {
  name = "${var.image_name}"
}

# Start the Container
resource "docker_container" "container_id" {
  name  = "${var.container_name}"
  image = "${docker_image.image_id.latest}"
  ports {
    internal = "${var.int_port}"
    external = "${var.ext_port}"
  }
}

#Output the IP Address of the Container
output "ip_address" {
  value       = "${docker_container.container_id.ip_address}"
  description = "The IP for the container."
}

output "container_name" {
  value       = "${docker_container.container_id.name}"
  description = "The name of the container."
}
</code></pre>
</li>
<li>
<p>Validate the changes:</p>
<p>terraform validate</p>
</li>
<li>
<p>Plan the changes:</p>
<p>terraform plan</p>
</li>
<li>
<p>Apply the changes using a variable:</p>
<p>terraform apply -var ‘ext_port=8080’</p>
</li>
<li>
<p>Change the container name:</p>
<p>terraform apply -var ‘container_name=ghost_blog’ -var ‘ext_port=8080’</p>
</li>
<li>
<p>Reset the environment:</p>
<p>terraform destroy -var ‘ext_port=8080’</p>
</li>
</ol>
</li>
<li>
<p><strong>Breaking Out Our Variables and Outputs</strong></p>
<ol>
<li>
<p>Edit <code>variables.tf</code>:</p>
<p>vi <a href="http://variables.tf">variables.tf</a></p>
<p><code>variables.tf</code> contents:</p>
<pre><code>#Define variables
variable "container_name" {
  description = "Name of the container."
  default     = "blog"
}
variable "image_name" {
  description = "Image for container."
  default     = "ghost:latest"
}
variable "int_port" {
  description = "Internal port for container."
  default     = "2368"
}
variable "ext_port" {
  description = "External port for container."
  default     = "80"
}
</code></pre>
</li>
<li>
<p>Edit <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code># Download the latest Ghost Image
resource "docker_image" "image_id" {
  name = "${var.image_name}"
}

# Start the Container
resource "docker_container" "container_id" {
  name  = "${var.container_name}"
  image = "${docker_image.image_id.latest}"
  ports {
    internal = "${var.int_port}"
    external = "${var.ext_port}"
  }
}
</code></pre>
</li>
<li>
<p>Edit <code>outputs.tf</code>:</p>
<p>vi <a href="http://outputs.tf">outputs.tf</a></p>
<p><code>outputs.tf</code> contents:</p>
<pre><code>#Output the IP Address of the Container
output "ip_address" {
  value       = "${docker_container.container_id.ip_address}"
  description = "The IP for the container."
}

output "container_name" {
  value       = "${docker_container.container_id.name}"
  description = "The name of the container."
}
</code></pre>
</li>
<li>
<p>Validate the changes:</p>
<pre><code>terraform validate
</code></pre>
</li>
<li>
<p>Plan the changes:</p>
<pre><code>terraform plan -out=tfplan -var container_name=ghost_blog
</code></pre>
</li>
<li>
<p>Apply the changes:</p>
<pre><code>terraform apply tfplan
</code></pre>
</li>
<li>
<p>Destroy deployment:</p>
<pre><code>terraform destroy -auto-approve -var container_name=ghost_blog
</code></pre>
</li>
</ol>
</li>
<li>
<p><strong>Maps and Lookups</strong></p>
<ol>
<li>
<p>Edit <code>variables.tf</code>:</p>
<p>vi <a href="http://variables.tf">variables.tf</a></p>
<p><code>variables.tf</code> contents:</p>
<pre><code>#Define variables
variable "env" {
  description = "env: dev or prod"
}
variable "image_name" {
  type        = "map"
  description = "Image for container."
  default     = {
    dev  = "ghost:latest"
    prod = "ghost:alpine"
  }
}

variable "container_name" {
  type        = "map"
  description = "Name of the container."
  default     = {
    dev  = "blog_dev"
    prod = "blog_prod"
  }
}

variable "int_port" {
  description = "Internal port for container."
  default     = "2368"
}
variable "ext_port" {
  type        = "map"
  description = "External port for container."
  default     = {
    dev  = "8081"
    prod = "80"
  }
}

</code></pre>
</li>
<li>
<p>Validate the change:</p>
<p>terraform validate</p>
</li>
<li>
<p>Edit <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code># Download the latest Ghost Image
resource "docker_image" "image_id" {
  name = "${lookup(var.image_name, var.env)}"
}

# Start the Container
resource "docker_container" "container_id" {
  name  = "${lookup(var.container_name, var.env)}"
  image = "${docker_image.image_id.latest}"
  ports {
    internal = "${var.int_port}"
    external = "${lookup(var.ext_port, var.env)}"
  }
}

</code></pre>
</li>
<li>
<p>Plan the <code>dev</code> deploy:</p>
<p>terraform plan -out=tfdev_plan -var env=dev</p>
</li>
<li>
<p>Apply the <code>dev</code> plan:</p>
<p>terraform apply tfdev_plan</p>
</li>
<li>
<p>Plan the <code>prod</code> deploy:</p>
<p>terraform plan -out=tfprod_plan -var env=prod</p>
</li>
<li>
<p>Apply the <code>prod</code> plan:</p>
<p>terraform apply tfprod_plan</p>
</li>
<li>
<p>Destroy <code>prod</code> deployment:</p>
<p>terraform destroy -var env=prod -auto-approve</p>
</li>
<li>
<p>Use environment variables:</p>
<p>export TF_VAR_env=prod</p>
</li>
<li>
<p>Open the Terraform console:</p>
</li>
</ol>
<pre><code>terraform console
</code></pre>
<ol start="11">
<li>Execute a lookup:</li>
</ol>
<pre><code>lookup(var.ext_port, var.env)
</code></pre>
<ol start="12">
<li>Exit the console:</li>
</ol>
<pre><code>unset TF_VAR_env
</code></pre>
</li>
<li>
<p>Workspaces</p>
<ol>
<li>
<p>Create a <code>dev</code> workspace:</p>
<p>terraform workspace new dev</p>
</li>
<li>
<p>Plan the <code>dev</code> deployment:</p>
<p>terraform plan -out=tfdev_plan -var env=dev</p>
</li>
<li>
<p>Apply the <code>dev</code> deployment:</p>
<p>terraform apply tfdev_plan</p>
</li>
<li>
<p>Change workspaces:</p>
<p>terraform workspace new prod</p>
</li>
<li>
<p>Plan the <code>prod</code> deployment:</p>
<p>terraform plan -out=tfprod_plan -var env=prod</p>
</li>
<li>
<p>Apply the <code>prod</code> deployment:</p>
<p>terraform apply tfprod_plan</p>
</li>
<li>
<p>Select the default workspace:</p>
<p>terraform workspace select default</p>
</li>
<li>
<p>Find what workspace we are using:</p>
<p>terraform workspace show</p>
</li>
<li>
<p>Select the <code>dev</code> workspace:</p>
<p>terraform workspace select dev</p>
</li>
<li>
<p>Destroy the <code>dev</code> deployment:</p>
</li>
</ol>
<pre><code>terraform destroy -var env=dev
</code></pre>
<ol start="11">
<li>Select the <code>prod</code> workspace:</li>
</ol>
<pre><code>terraform workspace select prod
</code></pre>
<ol start="12">
<li>Destroy the <code>prod</code> deployment:</li>
</ol>
<pre><code>terraform destroy -var env=prod
</code></pre>
</li>
<li>
<p><strong>Null Resources and Local-exec</strong></p>
<ol>
<li>
<p>Edit <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code># Download the latest Ghost Image
resource "docker_image" "image_id" {
  name = "${lookup(var.image_name, var.env)}"
}

# Start the Container
resource "docker_container" "container_id" {
  name  = "${lookup(var.container_name, var.env)}"
  image = "${docker_image.image_id.latest}"
  ports {
    internal = "${var.int_port}"
    external = "${lookup(var.ext_port, var.env)}"
  }
}

resource "null_resource" "null_id" {
  provisioner "local-exec" {
    command = "echo ${docker_container.container_id.name}:${docker_container.container_id.ip_address} &gt;&gt; container.txt"
  }
}

</code></pre>
</li>
<li>
<p>Reinitialize Terraform:</p>
<p>terraform init</p>
</li>
<li>
<p>Validate the changes:</p>
<p>terraform validate</p>
</li>
<li>
<p>Plan the changes:</p>
<p>terraform plan -out=tfplan -var env=dev</p>
</li>
<li>
<p>Apply the changes:</p>
<p>terraform apply tfplan</p>
</li>
<li>
<p>View the contents of <code>container.txt</code>:</p>
<p>cat container.txt</p>
</li>
<li>
<p>Destroy the deployment:</p>
<p>terraform destroy -auto-approve -var env=dev</p>
</li>
</ol>
</li>
<li>
<p><strong>Terraform Modules</strong></p>
</li>
<li>
<p>Basic Module Directory Setup</p>
<ol>
<li>
<p>Set up the environment:</p>
<p>mkdir -p modules/image<br>
mkdir -p modules/container</p>
</li>
<li>
<p>Create files for the image:</p>
<p>cd ~/terraform/basics/modules/image<br>
touch <a href="http://main.tf">main.tf</a> <a href="http://variables.tf">variables.tf</a> <a href="http://outputs.tf">outputs.tf</a></p>
</li>
<li>
<p>Create files for container:</p>
<p>cd ~/terraform/basics/modules/contain</p>
</li>
</ol>
</li>
<li>
<p>The Image Module</p>
<ol>
<li>
<p>Go to the image directory:</p>
<p>cd ~/terraform/basics/modules/image</p>
</li>
<li>
<p>Edit <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code># Download the Image
resource "docker_image" "image_id" {
  name = "${var.image_name}"
}

</code></pre>
</li>
<li>
<p>Edit <code>variables.tf</code>:</p>
<p>vi <a href="http://variables.tf">variables.tf</a></p>
<p><code>variables.tf</code> contents:</p>
<pre><code>variable "image_name" {
  description = "Name of the image"
}

</code></pre>
</li>
<li>
<p>Edit <code>outputs.tf</code>:</p>
<p>vi <a href="http://outputs.tf">outputs.tf</a></p>
<p><code>outputs.tf:</code> contents:</p>
<pre><code>output "image_out" {
  value       = "${docker_image.image_id.latest}"
}

</code></pre>
</li>
<li>
<p>Initialize Terraform:</p>
<p>terraform init</p>
</li>
<li>
<p>Create the image plan:</p>
<p>terraform plan -out=tfplan -var ‘image_name=ghost:alpine’</p>
</li>
<li>
<p>Deploy the image using the plan:</p>
<p>terraform apply -auto-approve tfplan</p>
</li>
<li>
<p>Destroy the image:</p>
<p>terraform destroy -auto-approve -var ‘image_name=ghost:alpine’</p>
</li>
</ol>
</li>
<li>
<p>The Container Module</p>
<ol>
<li>
<p>Go to the container directory:</p>
<p>cd ~/terraform/basics/modules/container</p>
</li>
<li>
<p>Edit <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code># Start the Container
resource "docker_container" "container_id" {
  name  = "${var.container_name}"
  image = "${var.image}"
  ports {
    internal = "${var.int_port}"
    external = "${var.ext_port}"
  }
}
</code></pre>
</li>
<li>
<p>Edit <code>variables.tf</code>:</p>
<p>vi <a href="http://variables.tf">variables.tf</a></p>
<p><code>variables.tf</code> contents:</p>
<pre><code>#Define variables
variable "container_name" {}
variable "image" {}
variable "int_port" {}
variable "ext_port" {}
</code></pre>
</li>
<li>
<p>Edit <code>outputs.tf</code>:</p>
<p>vi <a href="http://outputs.tf">outputs.tf</a></p>
<p><code>outputs.tf</code> contents:</p>
<pre><code>#Output the IP Address of the Container
output "ip" {
  value = "${docker_container.container_id.ip_address}"
}

output "container_name" {
  value = "${docker_container.container_id.name}"
}
</code></pre>
</li>
<li>
<p>Initialize:</p>
<p>terraform init</p>
</li>
<li>
<p>Create the image plan:</p>
<p>terraform plan -out=tfplan -var ‘container_name=blog’ -var ‘image=ghost:alpine’ -var ‘int_port=2368’ -var ‘ext_port=80’</p>
</li>
<li>
<p>Deploy container using the plan:</p>
<p>terraform apply tfplan</p>
</li>
</ol>
</li>
<li>
<p>The Root Module</p>
<ol>
<li>
<p>Go to the module directory:</p>
<p>cd ~/terraform/basics/modules/<br>
touch {<a href="http://main.tf">main.tf</a>,<a href="http://variables.tf">variables.tf</a>,<a href="http://outputs.tf">outputs.tf</a>}</p>
</li>
<li>
<p>Edit <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code># Download the image
module "image" {
  source = "./image"
  image_name  = "${var.image_name}"
}

# Start the container
module "container" {
  source             = "./container"
  image              = "${module.image.image_out}"
  container_name     = "${var.container_name}"
  int_port           = "${var.int_port}"
  ext_port           = "${var.ext_port}"
}

</code></pre>
</li>
<li>
<p>Edit <code>variables.tf</code>:</p>
<p>vi <a href="http://variables.tf">variables.tf</a></p>
<p><code>variables.tf</code> contents:</p>
<pre><code>#Define variables
variable "container_name" {
  description = "Name of the container."
  default     = "blog"
}
variable "image_name" {
  description = "Image for container."
  default     = "ghost:latest"
}
variable "int_port" {
  description = "Internal port for container."
  default     = "2368"
}
variable "ext_port" {
  description = "External port for container."
  default     = "80"
}

</code></pre>
</li>
<li>
<p>Edit <code>outputs.tf</code>:</p>
<p>vi <a href="http://outputs.tf">outputs.tf</a></p>
<p><code>outputs.tf</code> contents:</p>
<pre><code>#Output the IP Address of the Container
output "ip" {
  value = "${module.container.ip}"
}

output "container_name" {
  value = "${module.container.container_name}"
}

</code></pre>
</li>
<li>
<p>Initialize Terraform:</p>
<p>terraform init</p>
</li>
<li>
<p>Create the image plan:</p>
<p>terraform plan -out=tfplan</p>
</li>
<li>
<p>Deploy the container using the plan:</p>
<p>terraform apply tfplan</p>
</li>
<li>
<p>Destroy the deployment:</p>
<p>terraform destroy -auto-approve</p>
</li>
</ol>
</li>
<li>
<p><strong>Managing Docker Networks</strong></p>
</li>
<li>
<p>Set up the environment:</p>
<p>mkdir -p ~/terraform/docker/networks<br>
cd terraform/docker/networks</p>
</li>
<li>
<p>Create the files:</p>
<p>touch {<a href="http://variables.tf">variables.tf</a>,<a href="http://image.tf">image.tf</a>,<a href="http://network.tf">network.tf</a>,<a href="http://main.tf">main.tf</a>}</p>
</li>
<li>
<p>Edit <code>variables.tf</code>:</p>
<p>vi <a href="http://variables.tf">variables.tf</a></p>
<p><code>variables.tf</code> contents:</p>
<pre><code>variable "mysql_root_password" {
  description = "The MySQL root password."
  default     = "P4sSw0rd0!"
}

variable "ghost_db_username" {
  description = "Ghost blog database username."
  default     = "root"
}

variable "ghost_db_name" {
  description = "Ghost blog database name."
  default     = "ghost"
}

variable "mysql_network_alias" {
  description = "The network alias for MySQL."
  default     = "db"
}

variable "ghost_network_alias" {
  description = "The network alias for Ghost"
  default     = "ghost"
}

variable "ext_port" {
  description = "Public port for Ghost"
  default     = "8080"
}

</code></pre>
</li>
<li>
<p>Edit <code>image.tf</code>:</p>
<p>vi <a href="http://image.tf">image.tf</a></p>
<p><code>image.tf</code> contents:</p>
<pre><code>resource "docker_image" "ghost_image" {
  name = "ghost:alpine"
}

resource "docker_image" "mysql_image" {
  name = "mysql:5.7"
}

</code></pre>
</li>
<li>
<p>Edit <code>network.tf</code>:</p>
<p>vi <a href="http://network.tf">network.tf</a></p>
<p><code>network.tf</code> contents:</p>
<pre><code>resource "docker_network" "public_bridge_network" {
  name   = "public_ghost_network"
  driver = "bridge"
}

resource "docker_network" "private_bridge_network" {
  name     = "ghost_mysql_internal"
  driver   = "bridge"
  internal = true
}

</code></pre>
</li>
<li>
<p>Edit <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code>resource "docker_container" "blog_container" {
  name  = "ghost_blog"
  image = "${docker_image.ghost_image.name}"
  env   = [
    "database__client=mysql",
    "database__connection__host=${var.mysql_network_alias}",
    "database__connection__user=${var.ghost_db_username}",
    "database__connection__password=${var.mysql_root_password}",
    "database__connection__database=${var.ghost_db_name}"
  ]
  ports {
    internal = "2368"
    external = "${var.ext_port}"
  }
  networks_advanced {
    name    = "${docker_network.public_bridge_network.name}"
    aliases = ["${var.ghost_network_alias}"]
  }
  networks_advanced {
    name    = "${docker_network.private_bridge_network.name}"
    aliases = ["${var.ghost_network_alias}"]
  }
}

resource "docker_container" "mysql_container" {
  name  = "ghost_database"
  image = "${docker_image.mysql_image.name}"
  env   = [
    "MYSQL_ROOT_PASSWORD=${var.mysql_root_password}"
  ]
  networks_advanced {
    name    = "${docker_network.private_bridge_network.name}"
    aliases = ["${var.mysql_network_alias}"]
  }
}

</code></pre>
</li>
<li>
<p>Initialize Terraform:</p>
<p>terraform init</p>
</li>
<li>
<p>Validate the files:</p>
<p>terraform validate</p>
</li>
<li>
<p>Build a plan:</p>
<p>terraform plan -out=tfplan -var ‘ext_port=8082’</p>
</li>
<li>
<p>Apply the plan:</p>
</li>
</ol>
<pre><code>    terraform apply tfplan
    
11.  Destroy the environment:
    
    terraform destroy -auto-approve -var 'ext_port=8082'
    
12.  Fixing `main.tf`
    
    `main.tf` contents:
    
    ```
    resource "docker_container" "mysql_container" {
      name  = "ghost_database"
      image = "${docker_image.mysql_image.name}"
      env   = [
        "MYSQL_ROOT_PASSWORD=${var.mysql_root_password}"
      ]
      networks_advanced {
        name    = "${docker_network.private_bridge_network.name}"
        aliases = ["${var.mysql_network_alias}"]
      }
    }
    
    resource "null_resource" "sleep" {
      depends_on = ["docker_container.mysql_container"]
      provisioner "local-exec" {
        command = "sleep 15s"
      }
    }
    
    resource "docker_container" "blog_container" {
      name  = "ghost_blog"
      image = "${docker_image.ghost_image.name}"
      depends_on = ["null_resource.sleep", "docker_container.mysql_container"]
      env   = [
        "database__client=mysql",
        "database__connection__host=${var.mysql_network_alias}",
        "database__connection__user=${var.ghost_db_username}",
        "database__connection__password=${var.mysql_root_password}",
        "database__connection__database=${var.ghost_db_name}"
      ]
      ports {
        internal = "2368"
        external = "${var.ext_port}"
      }
      networks_advanced {
        name    = "${docker_network.public_bridge_network.name}"
        aliases = ["${var.ghost_network_alias}"]
      }
      networks_advanced {
        name    = "${docker_network.private_bridge_network.name}"
        aliases = ["${var.ghost_network_alias}"]
      }
    }
    
    ```
    
13.  Build a plan:
    
    terraform plan -out=tfplan -var 'ext_port=8082'
    
14.  Apply the plan:
    
    terraform apply tfplan
</code></pre>
<ol start="12">
<li>
<p><strong>Managing Docker Volumes</strong></p>
</li>
<li>
<p>Setup an environment:</p>
<p>cp -r ~/terraform/docker/networks ~/terraform/docker/volumes<br>
cd …/volumes/</p>
</li>
<li>
<p>Create <code>volumes.tf</code>:</p>
<p>vi <a href="http://volumes.tf">volumes.tf</a></p>
<p><code>volumes.tf</code> contents:</p>
<pre><code>resource "docker_volume" "mysql_data_volume" {
  name = "mysql_data"
}
</code></pre>
</li>
<li>
<p>Edit <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code>resource "docker_container" "mysql_container" {
  name  = "ghost_database"
  image = "${docker_image.mysql_image.name}"
  env   = [
    "MYSQL_ROOT_PASSWORD=${var.mysql_root_password}"
  ]
  volumes {
    volume_name    = "${docker_volume.mysql_data_volume.name}"
    container_path = "/var/lib/mysql"
  }
  networks_advanced {
    name    = "${docker_network.private_bridge_network.name}"
    aliases = ["${var.mysql_network_alias}"]
  }
}

resource "null_resource" "sleep" {
  depends_on = ["docker_container.mysql_container"]
  provisioner "local-exec" {
    command = "sleep 15s"
  }
}

resource "docker_container" "blog_container" {
  name  = "ghost_blog"
  image = "${docker_image.ghost_image.name}"
  depends_on = ["null_resource.sleep", "docker_container.mysql_container"]
  env   = [
    "database__client=mysql",
    "database__connection__host=${var.mysql_network_alias}",
    "database__connection__user=${var.ghost_db_username}",
    "database__connection__password=${var.mysql_root_password}",
    "database__connection__database=${var.ghost_db_name}"
  ]
  ports {
    internal = "2368"
    external = "${var.ext_port}"
  }
  networks_advanced {
    name    = "${docker_network.public_bridge_network.name}"
    aliases = ["${var.ghost_network_alias}"]
  }
  networks_advanced {
    name    = "${docker_network.private_bridge_network.name}"
    aliases = ["${var.ghost_network_alias}"]
  }
}
</code></pre>
</li>
<li>
<p>Initialize Terraform:</p>
<p>terraform init</p>
</li>
<li>
<p>Validate the files:</p>
<p>terraform validate</p>
</li>
<li>
<p>Build a plan:</p>
<p>terraform plan -out=tfplan -var ‘ext_port=8082’</p>
</li>
<li>
<p>Apply the plan:</p>
<p>terraform apply tfplan</p>
</li>
<li>
<p>List Docker volumes:</p>
<p>docker volume inspect mysql_data</p>
</li>
<li>
<p>List the data in <code>mysql_data</code>:</p>
<p>sudo ls /var/lib/docker/volumes/mysql_data/_data</p>
</li>
<li>
<p>Destroy the environment:</p>
</li>
</ol>
<pre><code>    terraform destroy -auto-approve -var 'ext_port=8082'
</code></pre>
<ol start="13">
<li>
<p><strong>Using Secrets</strong></p>
</li>
<li>
<p>Setup the environment:</p>
<p>mkdir secrets<br>
cd secrets</p>
</li>
<li>
<p>Encode the password with Base64:</p>
<p>echo ‘p4sSWoRd0!’ | base64</p>
</li>
<li>
<p>Create <code>variables.tf</code>:</p>
<p>vi <a href="http://variables.tf">variables.tf</a></p>
<p><code>variables.tf</code> contents:</p>
<pre><code>variable "mysql_root_password" {
  default     = "cDRzU1dvUmQwIQo="
}

variable "mysql_db_password" {
  default     = "cDRzU1dvUmQwIQo="
}

</code></pre>
</li>
<li>
<p>Create <code>image.tf</code>:</p>
<p>vi <a href="http://image.tf">image.tf</a></p>
<p><code>image.tf</code> contents:</p>
<pre><code>resource "docker_image" "mysql_image" {
  name = "mysql:5.7"
}

</code></pre>
</li>
<li>
<p>Create <code>secrets.tf</code>:</p>
<p>vi <a href="http://secrets.tf">secrets.tf</a></p>
<p><code>secrets.tf</code> contents:</p>
<pre><code>resource "docker_secret" "mysql_root_password" {
  name = "root_password"
  data = "${var.mysql_root_password}"
}

resource "docker_secret" "mysql_db_password" {
  name = "db_password"
  data = "${var.mysql_db_password}"
}

</code></pre>
</li>
<li>
<p>Create <code>networks.tf</code>:</p>
<p>vi <a href="http://networks.tf">networks.tf</a></p>
<p><code>networks.tf</code> contents:</p>
<pre><code>resource "docker_network" "private_overlay_network" {
  name     = "mysql_internal"
  driver   = "overlay"
  internal = true
}

</code></pre>
</li>
<li>
<p>Create <code>volumes.tf</code>:</p>
<p>vi <a href="http://volumes.tf">volumes.tf</a></p>
<p><code>volumes.tf</code> contents:</p>
<pre><code>resource "docker_volume" "mysql_data_volume" {
  name = "mysql_data"
}

</code></pre>
</li>
<li>
<p>Create <code>main.tf</code>:</p>
<p>vi <a href="http://main.tf">main.tf</a></p>
<p><code>main.tf</code> contents:</p>
<pre><code>resource "docker_service" "mysql-service" {
  name = "mysql_db"

  task_spec {
    container_spec {
      image = "${docker_image.mysql_image.name}"

      secrets = [
        {
          secret_id   = "${docker_secret.mysql_root_password.id}"
          secret_name = "${docker_secret.mysql_root_password.name}"
          file_name   = "/run/secrets/${docker_secret.mysql_root_password.name}"
        },
        {
          secret_id   = "${docker_secret.mysql_db_password.id}"
          secret_name = "${docker_secret.mysql_db_password.name}"
          file_name   = "/run/secrets/${docker_secret.mysql_db_password.name}"
        }
      ]

      env {
        MYSQL_ROOT_PASSWORD_FILE = "/run/secrets/${docker_secret.mysql_root_password.name}"
        MYSQL_DATABASE           = "mydb"
        MYSQL_PASSWORD_FILE      = "/run/secrets/${docker_secret.mysql_db_password.name}"
      }

      mounts = [
        {
          target = "/var/lib/mysql"
          source = "${docker_volume.mysql_data_volume.name}"
          type   = "volume"
        }
      ]
    }
    networks = [
      "${docker_network.private_overlay_network.name}"
    ]
  }
}

</code></pre>
</li>
<li>
<p>Initialize Terraform:</p>
<p>terraform init</p>
</li>
<li>
<p>Validate the files:</p>
</li>
</ol>
<pre><code>    terraform validate
    
11.  Build a plan:
    
    terraform plan -out=tfplan
    
12.  Apply the plan:
    
    terraform apply tfplan
    
13.  Find the MySQL container:
    
    docker container ls
    
14.  Use the `exec` command to log into the MySQL container:
    
    docker container exec -it [CONTAINER_ID] /bin/bash
    
15.  Access MySQL:
    
    mysql -u root -p
    
16.  Destroy the environment:
    
    terraform destroy -auto-approve
</code></pre>
<ol start="14">
<li>
<p><strong>Terraform Remote State</strong></p>
</li>
<li>
<p>Create an S3 Bucket</p>
<ol>
<li>
<p>Search for S3 in <strong>Find Services</strong>.</p>
</li>
<li>
<p>Click <strong>Create Bucket</strong>.</p>
</li>
<li>
<p>Enter a <strong>Bucket name</strong>. The bucket name must be unique.</p>
</li>
<li>
<p>Make sure the <em>Region</em> is <strong>US East (N. Virginia)</strong> Click <strong>Next</strong>.</p>
</li>
<li>
<p>Click <strong>Next</strong> again on the Configure options page.</p>
</li>
<li>
<p>Click <strong>Next</strong> again on the Set permissions page.</p>
</li>
<li>
<p>Click <strong>Create bucket</strong> on the Review page.</p>
</li>
</ol>
</li>
<li>
<p>Add the Terraform Folder to the Bucket</p>
<ol>
<li>
<p>Click on the bucket name.</p>
</li>
<li>
<p>Click <strong>Create folder</strong>.</p>
</li>
<li>
<p>Enter <strong>terraform-aws</strong> for the folder name.</p>
</li>
<li>
<p>Click <strong>Save</strong>.</p>
</li>
</ol>
</li>
<li>
<p>Add Backend to Your Scripts</p>
<ol>
<li>
<p>From the Docker Swarm Manager navigate to the AWS directory:</p>
<p>cd ~/terraform/AWS</p>
</li>
<li>
<p>Set the Environment Variables</p>
<p>export AWS_ACCESS_KEY_ID="[ACCESS_KEY]"<br>
export AWS_SECRET_ACCESS_KEY="[SECRET_KEY]]"<br>
export AWS_DEFAULT_REGION=“us-east-1”</p>
</li>
<li>
<p>Create <code>terraform.tf</code>:</p>
<pre><code>vi terraform.tf

</code></pre>
<p><code>terraform.tf</code> contents:</p>
<pre><code>terraform {
  backend "s3" {
    key    = "terraform-aws/terraform.tfstate"
  }
}

</code></pre>
</li>
<li>
<p>Initialize Terraform:</p>
<p>terraform init -backend-config “bucket=[BUCKET_NAME]”</p>
</li>
<li>
<p>Validate changes:</p>
<p>terraform validate</p>
</li>
<li>
<p>Plan the changes:</p>
<p>terraform plan</p>
</li>
<li>
<p>Apply the changes:</p>
<p>terraform apply -auto-approve</p>
</li>
<li>
<p>Destroy environment:</p>
<p>terraform destroy -auto-approve</p>
</li>
</ol>
</li>
</ol>

