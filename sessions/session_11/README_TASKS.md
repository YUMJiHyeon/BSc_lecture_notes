-----------

# Your turn now!

<img src="https://media.giphy.com/media/13GIgrGdslD9oQ/giphy.gif" width=50%/>

  - [1) Infrastructure as Code](#1-infrastructure-as-code)
  - [2) Optional: Availability and Scaling Revisited](#2-optional-availability-and-scaling-revisited)
  - [3) Software Maintenance](#3-software-maintenance)


## 1) Infrastructure as Code

Make sure that creation of your current and complete infrastructure is automated and up-to-date.
You decide how to do it. You might want to rely on the tools that we discussed in [Session 03](../session_03/Slides.md)
- Using Vagrant (can do most of the things that are required)
- Using shell scripts that use either
  a) the web-API of the VM provider
  b) the command line tool of the provider, e.g., [doctl](https://docs.digitalocean.com/reference/doctl/) for DigitalOcean
- Using a wrapper of the provider's web-API, in the programming language of your choice, e.g., [DigitalOcean's official Ruby API wrapper](https://rubygems.org/gems/droplet_kit), a [Python DigitalOcean API wrapper](https://pypi.org/project/python-digitalocean), etc.

In essence, this task is nothing new.
You encoded your [infrastructure as code already in session 03](../session_03/README_TASKS.md#1-implement-an-api-for-the-simulator-in-your-itu-minitwit).
The purpose of this task is to make sure that your IaC is up to date and can (re-)create your actual infrastructure.


### _Optional_: Encode Infrastructure as Code with OpenTofu/Terraform

In case you have energy and resources left, refactor your IaC code to HCL, i.e., so that you use a tool like OpenTofu/Terraform.
Do not worry in case you do not have energy and resources for this task.
Having a solution described above is good too.


## 2) _Optional_: Availability and Scaling Revisited

In case you have energy and resources left, and in case you consider your scaling scripts from last week to be to cumbersome, consider to refactor your _ITU-MiniTwit_ system to be deployed on a Docker Swarm Mode cluster.
Do not worry in case you do not have energy and resources for this task.
Having a high-availability setup and scaling scripts as [described in last week's task](../session_10/README_TASKS.md), is good for this course.


## 3) Software Maintenance

We are in software maintenance. That is, fix issues of your version of _ITU-MiniTwit_ **as soon as possible**. Let's say that as soon as possible means within 24 hours if possible, i.e., if it is not a super big issue that requires a big rewrite.

Now, with your monitoring and logging systems in place, you will likely observe issues when they arise or even before the arise. Just fix them as soon as you realize them.

Continue to release (now likely automatically) at least once per week versions of your system with corresponding fixes.
