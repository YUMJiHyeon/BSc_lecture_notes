class: center, middle

<img src="https://apriko.com/en/wp-content/uploads/sites/3/2024/12/devops.png" width=50%/>

# DevOps, Software Evolution and Software Maintenance

Helge Pfeiffer, Associate Professor,<br>
[Research Center for Government IT](https://www.itu.dk/forskning/institutter/institut-for-datalogi/forskningscenter-for-offentlig-it),<br>
[IT University of Copenhagen, Denmark](https://www.itu.dk)<br>
`ropf@itu.dk`

---

class: center, middle

# Feedback: The state of your projects?

---

### Release Activity

<object width="100%" data="http://209.38.211.172/release_activity_weekly.svg"></object>

---

### Weekly Commit Activity

<object width="100%" data="http://209.38.211.172/commit_activity_weekly.svg"></object>

---

### Latest processed events?

<object width="100%" data="http://64.226.108.122/chart.svg"></object>

---

### Error plot

<object width="100%" data="http://64.226.108.122/error_chart.svg"></object>

---

## How do you feel it is going with your projects?

---

### Building Dependable Software Systems

<img src="../session_09/images/dependability.png" width="100%">

Image source: I. Sommerville _"Software Engineering"_ (10th Ed.)

---

### Motivation: healthcare.gov

Highly anticipated launch of US American [healthcare.gov](https://www.healthcare.gov/).
During the first day, [_"the site was unable to handle the large volume of web traffic on the first day of its launch."_](https://federalnewsnetwork.com/technology-main/2025/07/how-healthcare-gov-botched-rollout-led-to-a-digital-services-revolution-in-government/)

<img src="images/healthcare_gov.png" style="width: 30%; float:right; margin: 20px;">


> Instead of new choices, the website told him to wait. Attempts to log on with a CBS News producer's iPad failed too. 
> After more than an hour, he gave up.
> "I was excited to get on, and I can't, so yeah I'm disappointed," Matt Warren said.
> Matt Warren said he will try again Wednesday. There are about six million uninsured residents in Texas. It's estimated half of them could be covered by the Affordable Care Act.
>
>
> [W. Andrews, A. Werner _"Healthcare.gov plagued by crashes on 1st day"_](https://www.cbsnews.com/news/healthcaregov-plagued-by-crashes-on-1st-day/)

--

How do we technically describe what happened?
The system was not available, i.e., had _low availability_.

---

### What is availability?

> There are five principal dimensions to **dependability**:
>
> 1. **Availability** [...] the probability that it will be up and running and able to deliver useful services to users at any given time.
> 2. **Reliability** [...] the probability, over a given period of time, that the system will correctly deliver services as expected by the user.
> 3. **Safety** [...] how likely it is that the system will cause damage to people or its environment.
> 4. **Security** [...] how likely it is that the system can resist accidental or deliberate intrusions.
> 5. **Resilience** [...] how well that ­system can maintain the continuity of its critical services in the presence of ­disruptive events, such as equipment failure and cyberattacks.
>
> I. Sommerville _"Software Engineering"_ (10th Ed.)

---

### What is availability?

> **availability.**
>
> (1) capability of a product to be operational and accessible when required for use
> [ISO/IEC 25010:2023, Systems and software engineering--Systems and software Quality Requirements and Evaluation (SQuaRE)--Product quality model, 3.5.2](https://www.iso.org/obp/ui/en/#iso:std:iso-iec:25010:ed-2:v1:en)
>
> (2) ratio of uptime divided by the sum of uptime plus downtime
>
> [IEEE 982:2024, Standard for Measures of the Software Aspects of Dependability, 3.1](https://ieeexplore.ieee.org/document/10745903)
>
> (3) degree to which a cloud service is accessible and usable upon demand by an authorized entity
> [ISO/IEC TS 25052-1:2022, Systems and software engineering--Systems and software Quality Requirements and Evaluation (SQuaRE): cloud services--Part 1: Quality model, 3.1.4.1](https://www.iso.org/obp/ui/en/#iso:std:iso-iec:ts:25052:-1:ed-1:v1:en)
>
> (4) degree to which an IT service is available to users when needed [ISO/IEC TS 25011:2017 Information technology--Systems and software Quality Requirements and Evaluation (SQuaRE)--Service quality models, 3.2.4.3](https://www.iso.org/obp/ui/en/#iso:std:iso-iec:ts:25011:ed-1:v2:en)
>
> (5) ability of an application object to perform its required function at an agreed instant or over an agreed period of time Example: _uptime/(uptime + downtime)_
> [ISO/IEC 16350-2015 Information technology--Systems and software engineering--Application management, 4.7](https://www.iso.org/obp/ui/en/#iso:std:iso-iec:16350:ed-1:v1:en)


--


> Availability is a quantitative component of dependability, expressed as a requirement parameter (threshold), as a probability (prediction or estimate), or as a measurement obtained during test or in-service operation (observation).
>
> https://pascal.computer.org/sev_display/search.action;jsessionid=Dx3w1o_lcuI-NWTfdqJ1SPKj2T6o8aN27qkWkomB.ip-10-100-95-168

---

### Availability: "number of nines"


<table style="text-align:right;">
<tbody><tr>
<th>Availability&nbsp;%
</th>
<th>t<sub>down</sub>/yr
</th>
<th>t<sub>down</sub>/mth
</th>
<th>t<sub>down</sub>/w
</th>
<th>t<sub>down</sub>/d
</th></tr>
<tr style="font-weight:bold;">
<td align="left">90% ("one nine")
</td>
<td>36.53d
</td>
<td>73.05h
</td>
<td>16.80h
</td>
<td>2.40h
</td></tr>
<tr>
<td align="left">95% ("one nine five")
</td>
<td>18.26d
</td>
<td>36.53h
</td>
<td>8.40h
</td>
<td>1.20h
</td></tr>
<tr>
<td align="left">97% ("one nine seven")
</td>
<td>10.96d
</td>
<td>21.92h
</td>
<td>5.04h
</td>
<td>43.20m
</td></tr>
<tr>
<td align="left">98% ("one nine eight")
</td>
<td>7.31d
</td>
<td>14.61h
</td>
<td>3.36h
</td>
<td>28.80m
</td></tr>
<tr style="font-weight:bold;">
<td align="left">99% ("two nines")
</td>
<td>3.65d
</td>
<td>7.31h
</td>
<td>1.68h
</td>
<td>14.40m
</td></tr>
<tr>
<td align="left">99.5% ("two nines five")
</td>
<td>1.83d
</td>
<td>3.65h
</td>
<td>50.40m
</td>
<td>7.20m
</td></tr>
<tr>
<td align="left">99.8% ("two nines eight")
</td>
<td>17.53h
</td>
<td>87.66m
</td>
<td>20.16m
</td>
<td>2.88m
</td></tr>
<tr style="font-weight:bold;">
<td align="left">99.9% ("three nines")
</td>
<td>8.77h
</td>
<td>43.83m
</td>
<td>10.08m
</td>
<td>1.44m
</td></tr>
<tr>
<td align="left">99.95% ("three nines five")
</td>
<td>4.38h
</td>
<td>21.92m
</td>
<td>5.04m
</td>
<td>43.20s
</td></tr>
<tr style="font-weight:bold;">
<td align="left">99.99% ("four nines")
</td>
<td>52.60m
</td>
<td>4.38m
</td>
<td>1.01m
</td>
<td>8.64s
</td></tr>
<tr>
<td align="left">99.995% ("four nines five")
</td>
<td>26.30m
</td>
<td>2.19m
</td>
<td>30.24s
</td>
<td>4.32s
</td></tr>
<tr style="font-weight:bold;">
<td align="left">99.999% ("five nines")
</td>
<td>5.26m
</td>
<td>26.30s
</td>
<td>6.05s
</td>
<td>864.00ms
</td></tr>
<tr style="font-weight:bold;">
<td align="left">99.9999% ("six nines")
</td>
<td>31.56s
</td>
<td>2.63s
</td>
<td>604.80ms
</td>
<td>86.40ms
</td></tr>
<tr style="font-weight:bold;">
<td align="left">99.99999% ("seven nines")
</td>
<td>3.16s
</td>
<td>262.98ms
</td>
<td>60.48ms
</td>
<td>8.64ms
</td></tr>
<tr style="font-weight:bold;">
<td align="left">99.999999% ("eight nines")
</td>
<td>315.58ms
</td>
<td>26.30ms
</td>
<td>6.05ms
</td>
<td>864.00μs
</td></tr>
<tr style="font-weight:bold;">
<td align="left">99.9999999% ("nine nines")
</td>
<td>31.56ms
</td>
<td>2.63ms
</td>
<td>604.80μs
</td>
<td>86.40μs
</td></tr>
<tr>
<td align="left">99.99999999% ("ten nines")
</td>
<td>3.16ms
</td>
<td>262.80μs
</td>
<td>60.48μs
</td>
<td>8.64μs
</td></tr>
<tr>
<td align="left">99.999999999% ("eleven nines")
</td>
<td>315.58μs
</td>
<td>26.28μs
</td>
<td>6.05μs
</td>
<td>864.00ns
</td></tr>
<tr>
<td align="left">99.9999999999% ("twelve nines")
</td>
<td>31.56μs
</td>
<td>2.63μs
</td>
<td>604.81ns
</td>
<td>86.40ns
</td></tr></tbody></table>

Adapted from: [Wikipedia](https://en.wikipedia.org/wiki/High_availability)

---

### Availability ≠ Uptime

Note, usually availability and uptime denote different metrics.

> The terms uptime and availability are often used interchangeably but do not always refer to the same thing. For example, a system can be "up" with its services not "available" in the case of a network outage. Or a system undergoing software maintenance can be "available" to be worked on by a system administrator, but its services do not appear "up" to the end user or customer.
>
> [Wikipedia](https://en.wikipedia.org/wiki/High_availability)

--

_Availability_ is especially relevant in the context of
- healthcare
- mission-critical systems
- banks
- online services and apps
- cloud-based applications

---

### How do systems fail to achieve availability? SPOF

This is probably the architecture that many of your systems have at the moment.

<img src="images/possible_arch1.png" width="100%">

Such an architecture has a **single point of failure** (SPOF) = *a part of the system failing will stop the entire system from working*.

> single points of failure, [is any] element that, if it failed, would have consequences affecting several things.
> Further, for there to be a single point of failure, there must be no backup system.
> If a single point of failure breaks, it takes out communication with a section of the network.
>
> [K. Dooley _"Designing Large Scale Lans: Help for Network Designers"_](https://dl.acm.org/doi/book/10.5555/504202)

---

### How do systems fail to achieve availability? SPOF

This scenario has different containers run on different nodes.

<img src="images/possible_arch2.png" width="100%">

--

From an availability point-of-view, this architecture is not an improvement.
It might even be worse, possessing more **single points of failure**.
Each node is one such possible point of failure.

---

### How do systems fail to achieve availability? Congestion


Imagine, your user authentication system is slow, and your application becomes really popular with many users trying to create accounts at the same time.
The server’s CPU becomes a **bottleneck** since hashing algorithms used by the application are computationally intensive, causing login delays, and users going away from the system.

--

  > Network traffic **congestion** occurs when demand for network resources exceeds available capacity, resulting in slow data transmission, high latency, and potential data loss.
  >
  > Common causes of congestion include increased user demand, limited bandwidth, hardware limitations, inefficient network configurations, and unexpected traffic spikes.
  >
  > To maintain reliable network performance, organizations should monitor network traffic, identify root causes, and implement proactive management strategies such as capacity planning, quality-of-service policies, traffic shaping, and infrastructure upgrades.
  >
  > [C. Kidd and M. Raza _"Understanding Network Traffic & Network Congestion: Metrics, Measurement, and Optimization"_](https://www.splunk.com/en_us/blog/learn/network-traffic-congestion.html)


Possible Reasons for congestion
  - Highly anticipated launches (healthcare.gov)
  - Traffic surges (e.g. [The Slashdot effect](https://en.wikipedia.org/wiki/Slashdot_effect), etc.)
  - Lack of monitoring

---

### What to do about availability? Addressing Congestion

First consider **performance optimization**.
That is, ensure that a system is designed and tuned to handle the expected load efficiently, reducing the risk of bottlenecks and failures.

For example,
- DB Indexes
- Suitable data structures and algorithms
- No unnecessary and wasteful computations

---

### What to do about availability? Addressing SPOF

In nature, important systems are replicated.

<img src="https://cdn.mos.cms.futurecdn.net/ARWms77gyVZ5u2MZkQqcKc-1256-80.jpg.webp" width="40%">

> On average, terrestrial plants in natural communities sustain 18% damage in the field. Individual plant species differ markedly in their ability to survive and reproduce after damage. Only 10% loss of leaf area significantly reduced fitness in Piper arieianum plants in the Costa Rican understory; in contrast, wild radish plants (Raphanus raphanistrum) can experience 25% leaf area loss without any concomitant drop in seed set.
>
> [S.Y. Strauss and A. A. Agrawal _"The ecology and evolution of plant tolerance to herbivory"_](https://www.sciencedirect.com/science/article/pii/S0169534798015766#BIB5)

Image source: [T. Spengler _"Hardwood Information: Recognizing Hardwood Tree Characteristics"_](https://www.gardeningknowhow.com/ornamental/trees/tgen/hardwood-tree-information.htm)

<!-- https://www.nature.com/scitable/knowledge/library/plant-resistance-against-herbivory-96675700/ -->

---

### Redundancy in System Design

Redundancy in system design is the solution to SPOF.

> **redundancy.** (1) in fault tolerance, the presence of auxiliary components in a system to perform the same or similar functions as other elements for the purpose of preventing or recovering from failures
>
> [ISO/IEC/IEEE 24765:2017 Systems and software engineering-Vocabulary](https://www.iso.org/obp/ui/en/#!iso:std:71952:en)

--

Trade-offs of redundancy

- **Cost**: it is more expensive
- **Synchronization**: keeping redundant components and data in sync, can be challenging, see, e.g., CAP theorem in your distributed systems course

Read more: [Tannenbaum and Van Steen's _Distributed Software Development_ Lectures](https://csis.pace.edu/~marchese/CS865/Lectures/Chap8/New8/Chapter8.html) on redundancy.

---

### Scaling

When performance optimizations and increase of redundancy do not suffice, one can **scale**.

--

There are two ways to scale:

1. **Vertical**
2. **Horizontal**

---

### Vertical Scaling

Replacing resources with larger or more powerful ones.

* Physical server: open the case and add more RAM, harddisk, network interfaces, etc.
* Virtual machine: reconfigure the VM programmatically


--


For example, after the first months of being hosted together with other applications on a small server, Stackoverflow scaled vertically to a single [dedicated server](https://stackoverflow.blog/2008/04/28/our-dedicated-server/) (2008) with the following specifications:

  * Windows Server 2008 Standard Edition x64
  * Dual Quad-Core Xeon E5320 (1.8 GHz)
  * 4 GB RAM
  * 271GB SAS hard drive

<!--
https://web.archive.org/web/20120324133732/http://teddziuba.com/2008/04/im-going-to-scale-my-foot-up-y.html
https://stackoverflow.blog/2009/01/25/new-stack-overflow-servers-ready/
https://stackoverflow.blog/2025/08/28/moving-the-public-stack-overflow-sites-to-the-cloud-part-1/
 -->

---

#### Example, Vertical Scaling with the VirtualBox GUI

1. **Power Off VM**
2. Modify RAM and storage (either via GUI or CLI)
3. **Power On VM**
4. From within the VM update the OS wrt your new disk size (takes a while!)

<img src="images/vertical-scaling-ui.png" width="50%">

Repartitioning, e.g., with `gparted` or similar tools.

---

#### Example, Vertical Scaling with VirtuaBox and CLI

```bash
$ VBoxManage list vms
"coursevm" {e072b310-1922-4113-93f5-2ca865e01722}
"lsd2018vm" {67fda2ea-7c3e-42f6-9a13-d0908020322d}
```

```bash
$ VBoxManage modifyvm "coursevm" --cpus 8
$ VBoxManage modifyvm "coursevm" --memory 8192
```

--

```bash
$ VBoxManage list hdds

UUID:           9953ea1b-7295-4547-94fa-209f49c258f5
Parent UUID:    base
State:          created
Type:           normal (base)
Location:       /path/to/node1ubuntu-16.04-amd64-disk001.vmdk
Storage format: VMDK
Capacity:       40960 MBytes
Encryption:     disabled
    ```

```sh
$ VBoxManage clonehd "9953ea1b-7295-4547-94fa-..." "cloned.vdi" --format vdi
$ VBoxManage modifymedium disk "cloned.vdi" --resize 65536
```

Optionally, you may want to convert the disk back to `vmdk` with `VBoxManage clonehd "cloned.vdi" "resized.vmdk" --format vmdk`

See, e.g., [modfication of RAM](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvm) or [modification of storage](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvd)

---

#### Example, Vertical Scaling with DigitalOcean

Similar to VirtualBox.

Note, you can only resize VMs that are not running.

<img src="https://docs.digitalocean.com/screenshots/droplets/pages/resize.b959b32afe0ed466b4d6db46731f842c5cde06105232581cd8a60e108844d67d.png" width="80%">

See https://www.digitalocean.com/docs/droplets/how-to/resize/#resizing-via-the-control-panel

---

#### Example, Vertical Scaling With the REST API of DigitalOcean

```bash
$ curl -X POST -H 'Content-Type: application/json' \
	   -H "Authorization: Bearer $DIGITAL_OCEAN_TOKEN" \
	   -d '{"type":"resize","size":"s-2vcpu-4gb"}' \
	   "https://api.digitalocean.com/v2/droplets/$DROPLET_ID/actions" | jq
```

*Notes:*
- $DIGITAL_OCEAN_TOKEN environment variable is defined
- $DROPLET_ID is defined
- Image types and sizes at: https://slugs.do-api.dev/


--


- Resizing CPU and RAM via API, automatically shuts down the droplet, so remember to start it again.

```bash
$ curl -X POST -H 'Content-Type: application/json' \
-H "Authorization: Bearer $DIGITAL_OCEAN_TOKEN" \
-d '{"type":"power_on"}' \
"https://api.digitalocean.com/v2/droplets/$DROPLET_ID/actions"
```

---

#### When is vertical scaling appropriate?

- Legacy systems, e.g., bank mainframes
- Some types of software that does not scale well horizontally, e.g., databases that don't cluster well
- Predictable growth: when you can anticipate the growth of demand on your system, and that growth can be serviced by the vertically scaled infrastructure


--


#### When is vertical scaling not appropriate?

- You have to adapt fast to varying workload (e.g., Black Friday)
- Complicated to scale down (often)
  - Slow: it implies switching machines off and on (both VM and physical)
- Some workloads are simply too big for vertical scaling
  - Facebook, Google, etc.
  - [Brief History of Scaling at LinkedIn](https://engineering.linkedin.com/architecture/brief-history-scaling-linkedin): *"An easy fix we did was classic vertical scaling ... While that bought some time, we needed to scale further"*
  - Scientific computing, e.g., seismic analysis, biotechnology, SETI@Home

---

### Horizontal Scaling

<img src="images/scaling-graphic.png" width="60%">

... increasing the number of computing nodes


--

Two aspects to horizontal scaling:

1. adding more machines to a setup
2. making all the machines share the responsibilities


---

#### Example Horizontal Scaling

For example, after a year on a single [dedicated server](https://stackoverflow.blog/2008/04/28/our-dedicated-server/), Stackoverflow scaled horizontally in 2009, https://stackoverflow.blog/2009/01/25/new-stack-overflow-servers-ready/

<img src="https://cdn.stackoverflow.co/images/jo7n4k8s/production/6d0317801ac039ffa1798772946b4bb179294af9-600x415.jpg" width="80%">

---

#### Example Horizontal Scaling

Two decades ago, the idea of horizontal scaling was a very revolutionary idea

- [As of **2000** Google can not host all their DB on a single machine](https://www.linkedin.com/pulse/how-did-google-scale-untold-story-shrey-batra/?trk=articles_directory).
- The only way that Google could keep up was by buying normal computers and wiring them together into a fleet.
- Because half the cost of these computers was considered junk—floppy drives, metal chassis—the company would order raw motherboards and hard drives and sandwich them together.
- To survive, Google would have to unite its computers into a seamless, resilient cluster.
- In **2004** they publish the paper [_"MapReduce: Simplified Data Processing on Large Clusters"_](https://www.usenix.org/legacy/events/osdi04/tech/full_papers/dean/dean.pdf) to propose an architecture for distributing the DB and subsequent queries over an array of machines.

---

### Horizontal Scaling with a Load Balancer

> Load balancing is the practice of distributing computational workloads between two or more computers. On the Internet, load balancing is often employed to divide network traffic among several servers. This reduces the strain on each server and makes the servers more efficient, speeding up performance and reducing latency. Load balancing is essential for most Internet applications to function properly.
>
> [_"What is load balancing?"_](https://www.cloudflare.com/learning/performance/what-is-load-balancing/)

<img src="https://doimages.nyc3.cdn.digitaloceanspaces.com/horizontal-scaling.png" width="80%">

Image source: [Horizontally Scaling PHP Applications](https://blog.digitalocean.com/horizontally-scaling-php-applications/)

---

#### Example Horizontal Scaling with a Load Balancer

In the exercise material, you get the following example:
 - A [basic web-application](https://github.com/itu-devops/scaling_exercises/blob/basic_scaling/application/info_server.go), which serves information about the name of the host it is running on, its process ID, and the port to which it listens.
 - You can inspect the setup in a respective [`Vagrantfile`](https://github.com/itu-devops/scaling_exercises/blob/basic_scaling/Vagrantfile).
 - And run it as in the following:

```bash
cd scaling_behind_nginx_load_balancer/
vagrant up
xdg-open http://192.168.33.10
```

<img src="images/local_scaling_lb.png" width="30%">

---

#### Example Horizontal Scaling with a Load Balancer
The application servers can be scaled up and down with a shell script [`scale_app.sh`](https://github.com/itu-devops/scaling_exercises/blob/basic_scaling/scale_app.sh)

```bash
vagrant ssh -c "/vagrant/scale_app.sh 3"
```

```bash
for i in 1 2 3; do curl -s http://192.168.33.10 | grep Port; done
            <li>Port: 8080</li>
            <li>Port: 8081</li>
            <li>Port: 8082</li>
```

<table>
    <tr>
        <td>
            <img src="images/local_scaling_lb.png" width="100%">
        </td>
        <td>
            <img src="images/local_scaling_lb2.png" width="100%">
        </td>
        <td>
            <img src="images/local_scaling_lb3.png" width="100%">
        </td>
</table>

---

#### Example Horizontal Scaling with a Load Balancer

- Note, when scaling an application server behind a load balancer like Nginx, you should not _restart_ the load balancer!
- Instead, _reload_ it, so that it is **gracefully** shutdown and restarted with the new configuration.
- That means, that pending requests will still be served and others will be kept on hold until application servers are up again.


--


- See how the script [`scale_app.sh`](https://github.com/itu-devops/scaling_exercises/blob/9fbe439d8ce8d43e8b73281cd0e443f769290e5a/scale_app.sh#L120) restarts the load balancer:
```bash
sudo systemctl reload nginx
```
- See the [documentation](https://nginx.org/en/docs/control.html)

---

### Horizontal Scaling with a Load Balancer

What is the problem with this setup?

<img src="https://doimages.nyc3.cdn.digitaloceanspaces.com/horizontal-scaling.png" width="80%">

--

Solves **scaling** and SPOF at the application server level but: Now the load balancer is the SPOF!

Image source: [Horizontally Scaling PHP Applications](https://blog.digitalocean.com/horizontally-scaling-php-applications/)

---

### Redundant Load Balancer Setup

How to make the balancer not anymore a single point of failure?

<img src="https://doimages.nyc3.cdn.digitaloceanspaces.com/ha-diagram-animated.gif" width="100%">

[Floating IP](https://blog.digitalocean.com/floating-ips-start-architecting-your-applications-for-high-availability/) (since 2022 called Reserved IP), is DigialOcean's name for static IPs ()

<!--
- Equivalents on other platforms, e.g. Elastic IPs @ Amazon
 -->

Image source: https://www.digitalocean.com/blog/floating-ips-start-architecting-your-applications-for-high-availability

---

#### Health Cheack via `keepalived`

> "Keepalived provides frameworks for both load balancing and high availability. [...] Keepalived implements a set of health checkers to dynamically and adaptively maintain and manage load balanced server pools according to their health. In addition, keepalived implements a set of hooks to the VRRP finite state machine providing low-level and high-speed protocol interactions."
>
> [`keepalived` documentation](http://keepalived.readthedocs.io/en/latest/introduction.html)

---

#### Health Cheack via `keepalived`

In the [exercise session](https://github.com/itu-devops/scaling_exercises/), you will experiment with a local high-availability setup, in which `keepalived` also provides a virtual IP comparable to DigitalOcean's "floating IP".


```
          Virtual IP: 192.168.20.100
                        |
              +---------+---------+
              |                   |
    lb1 (192.168.20.4)      lb2 (192.168.20.5)
 [Primary - Priority 255] [Backup - Priority 250]
              |                   |
              +---------+---------+
                        |
              +---------+---------+
              |                   |
    web1 (192.168.20.2)     web2 (192.168.20.3)
```

--

- `keepalived` manages the virtual IP (192.168.20.100) using VRRP (Virtual Router Redundancy Protocol) protocol
- The primary load balancer (lb1) holds the virtual IP by default
- If lb1 fails, lb2 automatically takes over the virtual IP
- Both load balancers use Nginx to distribute traffic to web servers
- Health checks ensure traffic only goes to healthy servers

---

### Redundant Load Balancer Setup

Links to relevant tutorials:

- [Load Balancing as a Service on DO](https://blog.digitalocean.com/load-balancers-simplifying-high-availability/)
- [HAProxy with Keepalived on Ubuntu](https://kifarunix.com/configure-highly-available-haproxy-with-keepalived-on-ubuntu-20-04)
- [An example of a high-availability setup with `keepalived` and Nginx](https://www.digitalocean.com/community/tutorials/how-to-set-up-highly-available-web-servers-with-keepalived-and-reserved-ips-on-ubuntu-14-04)
- [Heartbeat and Floating IP](https://www.digitalocean.com/community/tutorials/how-to-create-a-high-availability-setup-with-heartbeat-and-floating-ips-on-ubuntu-16-04)

---



### Your Turn! - Task: Scaling, likely you don't need it!

<img src="https://media.giphy.com/media/13GIgrGdslD9oQ/giphy.gif" width=40%/>

> hey is a tiny program that sends some load to a web application.
>
> https://github.com/rakyll/hey

- Download the binary for your host OS:
  * Linux (amd64): https://storage.googleapis.com/hey-releases/hey_linux_amd64
  * macOS (amd64): https://storage.googleapis.com/hey-releases/hey_darwin_amd64
  * Windows (amd64): https://storage.googleapis.com/hey-releases/hey_windows_amd64
- Navigate to the downloads directory or move the downloaded program to a directory on your PATH
- Now, conduct a basic load test against your _ITU-MiniTwit_ web-application:
  ```
  hey -n 1000 -c 50 http(s)://<your_application_url>
  ```
- What do you read out if the presented results?

---

### Load Testing

> Load testing is a type of software testing that helps ensure an application can handle expected workloads, while maintaining stable performance and providing a good end-user experience.
> [...]
> the primary objective is to simulate the average amount of activity on a system during a typical day in production.
>
> https://grafana.com/load-testing/load-testing-examples/


--


<img src="https://grafana.com/media/docs/k6-oss/chart-average-load-test-k6-script-example.png" width="100%">

Image source: https://grafana.com/load-testing/load-testing-examples/

---

### Types of Load Testing

<img src="https://grafana.com/media/docs/k6-oss/chart-load-test-types-overview.png" width="100%">

Image source: https://grafana.com/load-testing/load-testing-examples/

---

### Using `hey` as Tool for Basic Progressive Load Testing

`hey` reports metrics like:

- Requests/sec: Throughput
- Average response time: Mean latency
- Fastest/Slowest: Min/max latency
- Latency percentiles: p50, p90, p99
- Status code distribution: HTTP response codes

---

### Basic Progressive Load Testing

```bash
# Test 1: Light load (10 concurrent connections)
hey -n 1000 -c 10 -m GET http://192.168.33.10/ > results_c10.txt
# Test 2: Medium load (50 concurrent connections)
hey -n 1000 -c 50 -m GET http://192.168.33.10/ > results_c50.txt
# Test 3: Heavy load (100 concurrent connections)
hey -n 1000 -c 100 -m GET http://192.168.33.10/ > results_c100.txt
# Test 4: Very heavy load (200 concurrent connections)
hey -n 1000 -c 200 -m GET http://192.168.33.10/ > results_c200.txt
```

--

Let's consider the following exemplary load test results:

- Test 1: 10 concurrent connections:
  - Requests/sec: 500
  - 95%: 0.0234 secs
  - [200] 1000 responses, [500] 0 responses
- Test 2: 50 concurrent connections:
  - Requests/sec: 480
  - 95%: 0.0856 secs
  - [200] 1000 responses, [500] 0 responses
- Test 3: 100 concurrent connections:
  - Requests/sec: 350
  - 95%: 0. secs
  - [200] 980 responses, [500] 20 responses
- Test 4: 200 concurrent connections:
  - Requests/sec: 150
  - 95%: 2.1234 secs
  - [200] 850 responses, [500] 150 responses

---

### Basic Progressive Load Testing Interpretation

The 95% percentile means:
- 95% of requests completed within the reported time
- 5% of requests took longer than the reported time

That is, if, e.g. 95% `0.0234`, then
- 5% of requests take more than `0.0234` to be served
- As load increases and this number grows dramatically, it indicates the system is struggling
- The larger the gap between _Average_ and _95%_ percentile, the more variable (inconsistent) the performance of our web-application

```
Light load (10 concurrent):     95%: 0.0234 secs ✓ Good
Medium load (50 concurrent):    95%: 0.0856 secs ✓ Still OK
Heavy load (100 concurrent):    95%: 0.5432 secs ⚠️  Degrading
Very heavy (200 concurrent):    95%: 2.1234 secs ✗ Poor
```

---

### Using Load Testing to Guide Horizontal Scaling


1. Identify your target load: How many concurrent requests should the application support?
2. Run progressive load tests to identify when errors start to appear
3. Determine acceptable error rate: Is 0.5% acceptable? 1%?
4. Compare results with and without scaling:
  - Single instance results vs. five instances
  - See how much improvement scaling provides

--

Note, in industry, you would likely use more powerful load testing tools like [Grafana k6](https://grafana.com/docs/k6/latest/) or [Apache JMeter](https://jmeter.apache.org/)

---

## Problems with Horizontal Scaling

---

### Stateless vs. Stateful Services

There are two types of services

- **Stateless**
  - Does not maintain any internal state or data between requests.
  - Each request is handled independently
  - Ideal for horizontal scaling and load balancing.

- **Stateful**
  - Maintains internal state or data that persists across requests or instances
  - Examples include databases and file storage services
  - Replicating stateful services introduces challenges related to data consistency, synchronization, and failover

---

### Making your Applications Stateless

General principle: **a container should be disposable**.
If you can kill a container and spin up a new one without the user noticing, your state management is correct.

Your web-applications are not stateless yet.
Likely, you rely in cookies for user session management.

The problem when having such application instances behind a load balancer is, that a user, after logging in, might be redirected to an application instance on which she is not logged in yet.

---

<img src="https://miro.medium.com/v2/resize:fit:1100/format:webp/1*G8TvcDiT-C3nWGAXO9XsMQ.png" width="70%">

Image source https://medium.com/@aditimishra_541/sticky-sessions-an-in-depth-overview-4ec19bd7e22a

---

### One Solution: IP Hash-Based Sticky Sessions

Using Nginx's `ip_hash` directive to route requests based on the client's IP address to application servers.

```
upstream aspnet_backend {
    ip_hash;

    server 192.168.1.10:5000 weight=1;
    server 192.168.1.11:5000 weight=1;
    server 192.168.1.12:5000 weight=1;
}

server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://aspnet_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

See more [here](https://oneuptime.com/blog/post/2026-03-20-nginx-ip-hash-load-balancing-ipv4/view)

---

### Another Solution: Cookie-Based Sticky Sessions

Nginx's `sticky` module allows for cookie-based sticky sessions.
Drawback, only the Nginx Plus version has built-in support.
For open-source Nginx, the `sticky` directive requires additional configuration.

```
upstream aspnet_backend {
    sticky cookie srv_id expires=1h domain=example.com path=/ httponly secure;

    server 192.168.1.10:5000 weight=1 id=srv1;
    server 192.168.1.11:5000 weight=1 id=srv2;
    server 192.168.1.12:5000 weight=1 id=srv3;
}

server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://aspnet_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Connection "";
        proxy_http_version 1.1;
    }
}
```

See more [here](https://www.getpagespeed.com/server-setup/nginx/nginx-sticky-sessions)

---

### Yet Another Solution: Distributed Session Storage

Use for example an in memory database like [Redis](https://redis.io/) for distributed session storage.

```csharp
var builder = WebApplication.CreateBuilder(args);

// Register Redis as the distributed cache backend
builder.Services.AddStackExchangeRedisCache(options =>
{
    options.Configuration = builder.Configuration.GetConnectionString("Redis");
    options.InstanceName = "session:";
});

// Register session services
builder.Services.AddSession(options =>
{
    options.IdleTimeout = TimeSpan.FromMinutes(30);
    options.Cookie.HttpOnly = true;
    options.Cookie.IsEssential = true;
    options.Cookie.SecurePolicy = CookieSecurePolicy.Always;
});

var app = builder.Build();

app.UseRouting();
app.UseAuthentication();
app.UseAuthorization();
app.UseSession(); // Must come before MapControllers
app.MapControllers();
app.Run();
```

Source: https://oneuptime.com/blog/post/2026-03-31-redis-aspnet-core-session-state/view


Find other examples, [here](https://medium.com/@LuizAdolphs/asp-net-core-distributed-session-with-redis-8ce8bacf26cd), [here](https://www.c-sharpcorner.com/UploadFile/826da2/Asp-Net-session-state-management-with-redis-local-server-fa/
), [here](https://redis.io/solutions/session-management/), or [here](https://oneuptime.com/blog/post/2026-01-25-redis-session-storage/view)

---


## Upgrade Strategies for Scaled Applications

Two possible upgrade strategies:

1. Blue-Green
2. Rolling Updates

---

### Blue-green

- Two identical environments, where only one (green) is hot at any time
- Use the blue environment as staging environment for the final testing step for your next deployment

<img src="images/blue-green-fowler.png" width="30%">

Step by step:
  1. Currently deployed application (Green) is serving incoming traffic
  2. New version (Blue) is deployed and tested, but not yet receiving traffic
  3. When Blue is ready, load balancer starts sending incoming traffic to it too
  4. For a while: two different versions of the application run in parallel
  5. Load balancer stops sending incoming traffic to the "Green" and "Blue" is handling all the incoming traffic
  6. Green can now be safely removed
  7. Blue is marked as Green...

More about [colorful deployments](https://opensource.com/article/17/5/colorful-deployments)

---

### Rolling Upgrade

Deploy the upgrade iteratively

1. Stop the first application server
2. Replace it with a newer version
3. Start the new version of the upgraded application server
4. If upgrade of the application server fails pause the entire upgrade
5. Goto 1. and continue with the next application server

<img src="images/rolling.gif" width="50%">

---

## What to do now?

  * To prepare for your project work, practice with the [exercises](./README_EXERCISE.md)
  * Do the [project work](./README_TASKS.md) until the end of the week
