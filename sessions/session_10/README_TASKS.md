-----------


# Your turn now!

<img src="https://media.giphy.com/media/13GIgrGdslD9oQ/giphy.gif" width=50%/>

  - [1) Increase Availability of Your _ITU-MiniTwit_ Applications](#1-increase-availability-of-your-itu-minitwit-applications)
  - [2) Implement an Update Strategy](#2-implement-an-update-strategy)
  - [3) Software Maintenance](#3-software-maintenance)


## 1) Increase Availability of Your _ITU-MiniTwit_ Applications

Create a high-availability setup for your _ITU-MiniTwit_ application.
In such a setup, you would have two redundant load balancers serving multiple instances of your _ITU-MiniTwit_ applications.
As explained in class, only one of the load balancers is ever active at a time, i.e., there is no load balancer in front of either of them.
The setup should resemble [the one discussed in the lecture](https://www.digitalocean.com/community/tutorials/how-to-set-up-highly-available-web-servers-with-keepalived-and-floating-ips-on-ubuntu-14-04).


## 2) Scale _ITU-MiniTwit_ Horizontally and Implement an Update Strategy

To increase availability and capacity of your _ITU-MiniTwit_ system, scale your _ITU-MiniTwit_ applications horizontally.
That is, on each of the two web-servers in the high-availability setup, have at least two instances of the _ITU-MiniTwit_ web-application running (in case of high traffic or to reduce latency, you might have more than two instances).

As described in class, having multiple instances of your applications running behind a load balancer is likely posing issues with regards to user session handling.
Therefore, make sure to implement a solution to solve that problem, such as IP hashing, sticky sessions, or distributed session store.

Now that you have multiple instances of your _ITU-MiniTwit_ web-application running, implement an automatic update strategy for these in your CI pipeline.
Choose either rolling upgrades or blue-green upgrades.


## 3) Software Maintenance

We are in software maintenance. That is, fix issues of your version of _ITU-MiniTwit_ **as soon as possible**. Let's say that as soon as possible means within 24 hours if possible, i.e., if it is not a super big issue that requires a big rewrite.

Now, with your monitoring and logging systems in place, you will likely observe issues when they arise or even before the arise. Just fix them as soon as you realize them.

Continue to release (now likely automatically) at least once per week versions of your system with corresponding fixes.
