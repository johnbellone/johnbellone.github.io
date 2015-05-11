---
layout: post
title: Private Cloud at Home
tags: devops, cloud, openstack
nav: Blog
---
This weekend one of my colleagues at [Bloomberg][1] and I spent a few
hours at my apartment this weekend to deploy [OpenStack][2]. I made
the same attempt last year by myself and was barely able to get a
OpenStack service running. It was _that_ hard.  But this past year,
[with the help of a vibrant community][3], have made the process for
deploying a cluster a hell of a lot easier.

Using [Fuel from Mirantis][4], and with a little configuration of my
managed switch, I had a two node OpenStack cluster built from eBay
servers that I had lying around. One controller node and one compute
node we were ready to rock and roll. Even the managed switch
configuration for VLAN support went incredibly smooth.

The ultimate goal is to have a relatively portable, simple datacenter
so that distributed systems can be easily demonstrated at meetups. Chaz
and I will be working on making this process as transparent and automatic
as we can.

Even though my cluster is still in pieces on the floor I am hoping to
use it to demonstrate some [Chef][5] development at future
[Scale DC][6] meetups. Chaz will be presenting the work that he has
done setting up [Fuel][4] and his home cloud which puts my completely
to shame. After [ChefConf 2014][7] I am hoping to introduce some of
the work that the new [Web Operations team at Bloomberg][8] have been
hacking away at.

[1]: http://bloomberg.com/about/
[2]: http://openstack.org/
[3]: https://github.com/stackforge/
[4]: http://software.mirantis.com/
[5]: http://getchef.com/
[6]: https://scaledc.org/
[7]: http://chefconf.opscode.com/
[8]: http://thoughtlessbanter.com/2014/03/12/web-operations-at-bloomberg/
