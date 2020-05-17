---
title: Network Traffic Types
subtitle: Unicast, Broadcast, Multicast, and Anycast.
layout: post
---
**Unicat**

Most network traffic is unicast in nature, meaning that traffic travels from a single source deivce to another single destination device.
---
Note

BGP establish a TCP session between peers. Therefore, unicast transmissions are used for BGP route advertisement.
---

**Broadcast**

It travels from a single source to all destination in a subnet. It is used in IPV4 networks only.

**Multicast**

It is similar to broadcast, we want to provide an efficient mechanism for a single host to send traffic to multiple, yet specific destinations.

For example, imagine a network with 100 uses, 20% for a video server. With a unicast solution, the video server would have to send 20 individual streams, consuming a significant amount of network bandwidth. With a broadcast solution, the video server indeed only need to send the video stream once. But it is for everyone, even those devices not wanting it.
<img src="/img/posts/Multicast.png" alt="multicast" align="center"/>

**Anycast**

With it, a single IPV6 address is assigned to multiple devices.
