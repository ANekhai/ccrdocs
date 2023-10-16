# CCR's New Environment Explained  

CCR staff have been working for over a year to provide users with an updated environment that includes a new software infrastructure, new compute nodes, and a new operating system.  Additionally, a new core network switch and updated networking protocols have been put into place.  This combination of projects is what we're referring to as CCR's New Environment.  Each of these separately has been a monumental task and we've tried to orchestrate these updates while also keeping the existing infrastructure in place.  Now it's time for everyone to make the transition as the old infrastructure will be decommissioned this fall.  This transistion will involve changes for existing users.  We have tried to keep these changes as easy to navigate as possible, but change can be hard and we're here to help!

This page is intended to provide details to the changes users can expect and break down the experience each user might expect.  Whether you're a long time CCR user or brand new to our center, we hope to smooth out the process of onboarding to the new environment.  Please note this is just an overview document and users should refer to the wealth of information in the rest of our documentation website for all the details of using CCR's resources.  

We highly recommend you start by watching this presentation on CCR's new software modules and how to utilize the new environment:  

![type:video](https://youtube.com/embed/k1fymCTeI0k)   



Beginning August 31, 2023 CCR staff will host weekly office hours from 11am-12pm on Thursdays to provide support to users switching over to the new environment.  Please join us and bring your questions!  

```
https://buffalo.zoom.us/j/94613848883?pwd=Q2ZjU3VIaWZDZGZPdldjR1JwOUVmZz09 
Meeting ID: 946 1384 8883 
Passcode: 497161 
```
NOTE:  You must authenticate to Zoom prior to joining the meeting

## New Users 

Users new to CCR after August 8, 2023 will automatically be put into the new environment.  This means you don't need to do anything other than follow the directions [below](#the-new-resources) to access the new compute nodes and new OnDemand service.  If you are a member of a research group that owns their own nodes, you may not want to be in the new environment yet.  You may want to go back to the old environment so you can use your group's nodes until they are transitioned to the new environment.  [See here](#using-the-old-software) for guidance. 

!!! Note "ATTN: Faculty Cluster Users"  
    The faculty cluster nodes have not been transitioned into the new environment yet.  We will complete the transition of UB-HPC nodes first, install the newly purchased faculty nodes in the new environment next, and then transition the existing faculty cluster partitions last.  We will contact the owners of nodes in the faculty cluster as we begin to schedule this transition.  If you do not have many nodes in your partition, you may wish to switch to the new environment now to make use of CCR's new compute nodes in the UB-HPC cluster.  If want to continue to use your nodes, we provide [recommendations below](#the-new-resources) for how to work in both environments so you can begin migrating your software and workflows.  

## Existing Users - How to Transition 

- Create a file in your home directory named .ccr_new_modules.  Log out & back in again. -OR - use the new login server or OnDemand server as described [below](#the-new-resources)  
- Ensure that nothing has been added to the `.bashrc` file in your home directory.  Command aliases are usually fine; however, comment out or remove anything else not provided by CCR.  This is what your `.bashrc` file should look like:  
```
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi


if [ -f /etc/bash.bashrc ]; then
    . /etc/bash.bashrc
fi

# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'

    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

```
- Follow the directions [below](#the-new-resources) to access the new resources    
- If you have existing software modules you or your group have built, they will likely need to be re-built for this environment.  See [here](#existing-modules) for more information    


## Using the old software  
If you'd like to remain in the old environment until your group's nodes are transitioned into the new environment, remove the `~/.ccr_new_modules` file and log out and back into `vortex.ccr.buffalo.edu`  You should NOT use `vortex-future` or `ondemand-future` as both these services are only in the new environment.  You should also not use the `ubhpc-future` reservation to submit jobs as the nodes in that reservation are in the new environment and won't work with old modules.  

**What if I want to use my groups nodes AND the new environment?**  
We recommend that your research group test the new environment and begin migrating your software and workflows.  However, straddling the old and new environments may be difficult.  It will involve some manipulation on your part and your mileage may vary.  You may use `vortex-future.ccr.buffalo.edu` or https://ondemand-future.ccr.buffalo.edu to submit jobs to the UB-HPC compute nodes in the new environment.  Make sure you do not have the `.ccr_new_modules` file in your home directory.  When these jobs run they'll be using the new environment and any software modules you're loading will be from the new software stack.  You'll need to specify the new compute node reservation in your batch script (see below).  If you want to run on the old UB-HPC cluster nodes or nodes in the faculty cluster that have not been transitioned yet, submit jobs from `vortex.ccr.buffalo.edu` or using https://ondemand.ccr.buffalo.edu, not ondemand-future.  **Keep in mind** many software packages store libraries, cache files, and temporary files in your home directory so trying to use these two environments at the same time may not work.  This will all depend on what software you're using and will be a trial and error process on your part.  Good luck!


## The New Resources  

!!! Warning "REMINDER!!!"  
    Do NOT add anything to the `.bashrc` file in your home directory!  Loading modules, enabling conda environments, and other environment-related tasks will almost certainly break your environment on the CCR systems.  It will break CCR's quota tool, cause OnDemand desktops & apps to fail to start, and cause problems with batch scripts on compute nodes.  

**New Login Server**

You may use the new login server `vortex-future.ccr.buffalo.edu` during the transition.  Eventually all login servers will be setup like this one and you'll be able to access them in the pool using `vortex.ccr.buffalo.edu`  However, for now, the vortex pool has vortex1 and vortex2 that continue to have access to the old software modules.  


**New OnDemand**  

To access the new compute nodes and new software via OnDemand, we have installed [OnDemand 3.0](https://ondemand-future.ccr.buffalo.edu).  There are many new features to take advantage of, as well as changes to how we've laid out the apps.  Please [see here](../howto/ondemand.md) for more details.  You will ONLY have access to compute nodes that have been moved to the new environment and ONLY have access to the new software modules.  Faculty cluster nodes will not be available in OnDemand 3.0 until they've been migrated into the new environment.   

The new server URL is:  [https://ondemand-future.ccr.buffalo.edu](https://ondemand-future.ccr.buffalo.edu)


**Newest Compute Nodes**

The newest compute nodes available at CCR in the UB-HPC cluster have been put into a reservation for users to access them and the new environment.  You will need to specify the following in your batch scripts:  

```
#SBATCH --cluster=ub-hpc
#SBATCH --partition=general-compute
#SBATCH --qos=general-compute
#SBATCH --reservation=ubhpc-future
```

**Using `salloc`?** If you use `salloc` for interactive jobs, you must specify the reservation in your salloc command and run an additional command after being allocated a node:  

```
salloc --reservation=ubhpc-future --qos=general-compute --partition=general-compute  --job-name "MyJob" --nodes=1 --ntasks=1 --mem=8G --time=00:30:00  

srun --pty /bin/bash --login
```

!!! Tip "Module command errors"  
    Users submitting jobs to older avx2 architecture-based nodes in the faculty cluster may run into issues with the login node environment persisting into the job environment.  This may present with the error "module command not found."  Please contact [CCR Help](../help.md) for guidance.  The error "module not found" means the module is not available for the architecture of the node you're running on.  CCR's software modules are architecture dependent and many modules have not been built for avx2 nodes as these older nodes are being removed from the UB-HPC cluster. 


## Existing Modules  

Any modules previously created in the old system will need to be reinstalled into the new modules.  We know, this isn't what you wanted to hear.  We feel your pain.  We're currently trying to reconstruct 20+ years of software installations ourselves.  The reason behind this isn't so much a new version of modules but it's more about the operating system, compilers, and linking used to install your old software.  It is unlikely that this will work in the new operating system.  As part of the software infrastructure, CCR provides a compatiblity layer.  Installing software using this will allow software to work on any Linux-based operating system, no longer tying us (or you) to a specific flavor of Linux.  This is especially coming in handy with all the turmoil over RedHat derivatives we've seen lately.  This is future-proofing us and will allow for the testing of cutting edge operating systems in the future, which has been asked of us by researchers over the years.  If your software did not require building (using compilers) or linking to the system libraries (for example: python scripts), it MAY be POSSIBLE to convert them over to the new module directory structure so they are available to you.  At that point, you can test to see if the software works on compute nodes in the new environment.  This is not something CCR can provide support for; however, if you'd like to try it, you'd need your module(s) to be in the directory structure [defined here](../software/building.md#building-modules-for-your-group) (see specifically the tip in green).  

## What if we installed our own software?  

If you installed your own software without using modules, it is possible it might work.  However, it's the same basic concept as in the above paragraph.  With a new operating system, updated compilers, and the fact that your software was linked against old libraries, it is quite probable it will not work on the newly installed compute nodes.  You are absolutely welcome to try it though and we'll keep our fingers crossed for you that it does!  If your code can make use of different CPU architectures, you will want to optimize it by compiling it in CCR's new environment.

## Software Installation Requests  

CCR is accepting requests for software installations and encourages users to "like" any requests they see for software they want to use in [this list](https://github.com/ubccr/software-layer/issues).  This helps us to rank the requests and prioritize the order they are installed.  [Follow these instructions](../software/building.md#software-build-requests) to request a software build.  Currently, we have the staffing capacity only to install software available in the [EasyBuild recipe catalog](https://github.com/easybuilders/easybuild-easyconfigs/tree/develop/easybuild/easyconfigs). We can provide advice and troubleshooting assistance for groups needing to install outside of this environment via help tickets. 

We will be hosting office hours beginning in the next few weeks for anyone with questions about the new environment or how to build software for their groups.  More information will be posted on our communication channels soon.  