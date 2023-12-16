---
title: Google Cloud — Network Service Tiers
description: >-
  An overview about Google Cloud network tiers
date: '2021-02-05T09:07:31.692Z'
categories: ["network", "cloud", "tech"]
keywords: []
slug: /@itsmesunil/google-cloud-network-service-tiers-7fd23d3a536a
draft: false
---

![](/img/0__9zwhNMLG223Yy8v3.jpg)

A slow loading website is always frustrating. Well, there could be multiple factors which attribute to this behaviour. But the prime suspect for this is Latency.

The term Latency measure up to the time for data to be transmitted from the web server to the user’s computer and vice versa. This is measured in milliseconds. High latency causes the delay in page load speeds.

> A decade ago, Amazon found that every 100ms of latency cost them 1% in sales

What matters is the hardware and network infrastructure which connects these points. Google cloud has a global network that spans 22 regions, 67 zones,40 points of presence, and 96 CDN edge nodes. It has a global fibre network connecting you to the world. In this series we will allude to different network service tiers available in GCP.

Google offers two types of network service tiers:

1.  **Premium Tier:** This is the coolest feature that Google offers. This tier uses Google’s extensive fiber network. The traffic stays on Google’s own network for as long as possible. This is known as [cold-potato](https://en.wikipedia.org/wiki/Hot-potato_and_cold-potato_routing) routing. This lowers the number of trace route hops, faster transport and network latency.

![](/img/0__gNS3f0K8gGYux6UU.gif)

2. **Standard Tier:** In this tier the packet is going to stay more on public internet. This is called as hot-potato routing. As you can see in the above diagram, the packet takes more hops before reaching Google’s Point of Presence. This is what most other cloud providers are largely using.

Let’s get into action. For this we would create a two VM instances one with standard network tier and other with premium network tier respectively.

The network service tier can be selected in the networking tab while creating compute engine instances.

![](/img/1__50WrkVcrSfVUWvxiMw35sQ.png)

I also have created two compute engine VM’s, one which is uses _standard_ network tier and the other which uses _premium a_ network tier.

![](/img/1__x5BT__1y6BHsqvqIcpl0B4Q.png)

To check how many hops it would take to reach Google’s PoP, I have used

*   `traceroute` tool, which is a diagnostic tool used to track in real-time the pathway taken by a packet on an IP network from source to destination, reporting the IP addresses of all the routers it pinged in between

and check the ISP details:

*   You can use any site to get the ISP details ( here we used [www.showmyisp.com](http://www.showmyisp.com) )

In **Figure 1** you can see that when we tracked the routes of the VM (_vm-premium-tier_ ) which used the premium network tier, the packet reached the Google’s PoP in the 5th hop.

![](/img/1__yVy4fouCL9iRB__GKlHPCZQ.png)

**Figure 2** shows the path taken by the VM ( _vm-standard-tier_ )which used the standard network tier. An additional 5 hops was needed to reach Google’s PoP

![](/img/1__vkFt914sSqUJUvzfqY16Qg.png)

We can clearly see, in standard tier the packet stays in public internet for longer time. It takes longer time to enter Google’s PoP.

Hope this did explains the concept of the network service tiers. Please feel free to post your feedback/comments in the response section.