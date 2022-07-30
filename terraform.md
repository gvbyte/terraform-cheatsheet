<center><h1>terraform.tf</center>

<center><h2>About Terraform CLI (Command Line Interface)</h2></center>

<li>Terraform, a tool created by Hashicorp in 2014, written in Go (Golang), aimed to build, change and version control your infrastructure.

<li>This concept adapted the process of Infrastructure as Code (IaC), a process of managing and provisioning computer data through machine-readable files which can be version controlled and reused.

<li>This tool has a powerfull and very intuitive Command Line Interface. Leveraging 4-5 commands like GitHub to initiliaze, plan, apply, show, and destroy</li>
<center>
<h3>Basic Terraform IaC Workflow<h3>

![terraform flow](./designs/flow.png "terraform flow")
</center>
<center><h2>Installation<h2></center>

<h4>Chocolatey on Windows</h4>

* <a href="https://chocolatey.org">Chocolatey</a> is a free and open-source package management system for Windows. Install the Terraform package from the command-line.


```
$ choco install terraform
``` 

* Verify the installation using the --version flag or version command	

```
$ terraform version
Terraform vX.X.X
on OS_Architecture
``` 


<h4>Homebrew on macOS X (X64/arm64)</h4>


* <a href="https://brew.sh">Homebrew</a> is a free and open-source package management system for macOS. Install the Terraform package from the command-line.

```
$ brew install terraform 
``` 

* Second, verify the installation using the --version flag or version command	

```
$ terraform version
Terraform vX.X.X
on OS_Architecture
``` 



<h4>Linux - Ubuntu/Debian</h4>


* First, we will apply updates to our system to update any dependency needed for terraform, also doing you a favor :) 

```
$ sudo apt update
``` 

* Second, perform a apt-get to install terraform

```
$ sudo apt-get install terraform
``` 

* Third, verify installation via terraform version

```
$ terraform version
Terraform vX.X.X
on OS_Architecture
``` 

<center><h2>Usage<h2></center>

<h4>Help</h4>

* View all commands using terraform --help


```
$ terraform --help
Usage: terraform [global options] <subcommand> [args]

The available commands for execution are listed below.
The primary workflow commands are given first, followed by
less common or more advanced commands.

Main commands:
  init          Prepare your working directory for other commands
  validate      Check whether the configuration is valid
  plan          Show changes required by the current configuration
  apply         Create or update infrastructure
  destroy       Destroy previously-created infrastructure

All other commands:
  console       Try Terraform expressions at an interactive command prompt
  fmt           Reformat your configuration in the standard style
  force-unlock  Release a stuck lock on the current workspace
  get           Install or upgrade remote Terraform modules
  graph         Generate a Graphviz graph of the steps in an operation
  import        Associate existing infrastructure with a Terraform resource
  login         Obtain and save credentials for a remote host
  logout        Remove locally-stored credentials for a remote host
  output        Show output values from your root module
  providers     Show the providers required for this configuration
  refresh       Update the state to match remote systems
  show          Show the current state or a saved plan
  state         Advanced state management
  taint         Mark a resource instance as not fully functional
  test          Experimental support for module integration testing
  untaint       Remove the 'tainted' state from a resource instance
  version       Show the current Terraform version
  workspace     Workspace management

Global options (use these before the subcommand, if any):
  -chdir=DIR    Switch to a different working directory before executing the
                given subcommand.
  -help         Show this help output, or the help for a specified subcommand.
  -version      An alias for the "version" subcommand.


```


<h4>terraform init</h4>


* This command is needed to be executed to initialize the terraform *.tf file in the current directory
* No other command will work as this command installs:
	* Terraform modules
	* Backend files 
	* Provider(s) plugins



```
$ terraform init
``` 


<h4>terraform init</h4>


<h4>terraform providers</h4>


* This command shows you the list of providers required in current configuration


```
$ terraform providers

Providers required by configuration:
.
└── provider[registry.terraform.io/hashicorp/XXXXXXX]

``` 


