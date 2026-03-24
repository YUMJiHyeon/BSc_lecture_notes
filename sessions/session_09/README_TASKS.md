-----------

# Your turn now!

<img src="https://media.giphy.com/media/13GIgrGdslD9oQ/giphy.gif" width=50%/>

  - [1) Deploy a Reverse Proxy and Enable TLS Encryption](#1-deploy-a-reverse-proxy-and-enable-tls-encryption)
  - [2) Setup and Configure a Software Firewall on Your Servers](#2-setup-and-configure-a-software-firewall-on-your-servers)
  - [3) Enhance your CI Pipelines with multiple security related static analysis tools](#3-enhance-your-ci-pipelines-with-multiple-security-related-static-analysis-tools)
  - [4) Switch to Security Hardened Docker Containers in Production](#4-switch-to-security-hardened-docker-containers-in-production)
  - [5) Software Maintenance](#5-software-maintenance)


The general topic of this weeks project work is improve security of your systems.


## 1) Deploy a Reverse Proxy and Enable TLS Encryption

Deploy a reverse proxy to your application server and enable TLS encryption to the reverse proxy.
To start with, you might follow [our TLS tutorial](./TLSTutorial.md) that installs, Nginx and `certbot` directly on your server.
You might want to start with such a setup before also convert these two applications to Docker containers.


## 2) Setup and Configure a Software Firewall on Your Servers

Setup and configure a software firewall like `ufw` on your servers.
For example, do so with the advice from the following guides:

  - [DigitalOcean Tutorial: How to Set Up a Firewall with UFW on Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu)
  - [`ufw` Ubuntu Server documentation](https://ubuntu.com/server/docs/how-to/security/firewalls/)


## 3) Enhance your CI Pipelines with multiple security related static analysis tools

Add at least one static analysis tool that scans for security vulnerabilities in your application code.
That is, add a tool like [Security Code Scan](https://security-code-scan.github.io/), [CodeQL](https://codeql.github.com/docs/codeql-overview/about-codeql/), or [Semgrep](https://semgrep.dev/) with enabled security rules to your CI pipeline.

At a later build stage, add at least one other Docker image vulnerability scanner like [Trivy](https://trivy.dev/docs/latest/getting-started/), [Docker Scout](https://docs.docker.com/scout/), or [Snyk](https://docs.snyk.io/) to your CI pipeline.

Integrate such tools, so that build, delivery, and deployment get aborted as early as possible in a meaningful way, i.e., shift-left security.


## 4) Switch to Security Hardened Docker Images in Production

If possible, switch to security hardened Docker images in production.
Find a catalog of security hardened images on [DockerHub](https://hub.docker.com/hardened-images/catalog).

If there are no suitable images available, try to harden your images as much as possible within the given time of the project, using the [OWASP Docker Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Docker_Security_Cheat_Sheet.html).
Keep a log of the steps that you take for hardening your images.


## 5) Software Maintenance


We are in software maintenance. That is, fix issues of your version of _ITU-MiniTwit_ **as soon as possible**. Let's say that as soon as possible means within 24 hours if possible, i.e., if it is not a super big issue that requires a big rewrite.

Now, with your monitoring systems in place, you will likely observe issues when they arise or even before the arise. Just fix them as soon as you realize them.

Additionally, our dashboards illustrate status and potential errors as the simulator 'sees' them [here](http://64.226.108.122/status.html). For example, fix wrong status codes, e.g., `tweet` shall return `204` instead of `200`, or too slow response times.

Continue to release (now likely automatically) at least once per week versions of your system with corresponding fixes.
