---
title: Basic BGP configuration 
subtitle: eBGP vs iBGP
layout: post
---
Today, I am gonna dive into some easy build on BGP in GNS3.

The most important function of BGP is to work through different `autonomous system` and we have `AS_PATH` to decide the best path and to prevent loop between different AS. In BGP, we do not have 'metric' or 'cost', we use `path attributes` to decide best path.

Why we need iBGP, we need it to help propagate learned routes between edge routers. BGP is running on tcp port 179. In this case, when we see status `IDLE`, think about do you successfully finish tcp three-way handshake. Is there a firewall blocking tcp traffic.

When I was in interview, there is always questions like why do you choose BGP. The answer is simple. It is scalable and we have so many choices in `PA`. **YOU WILL NEED IT IF YOU WANT TO USE MPLS**.
[BGP GNS3 tutorial](https://github.com/hosseinoliabak/cisco/blob/master/Routing/06_01_bgp.md)
<img src="/img/posts/basic_bgp.png" alt="simple configuration" align="center"/>
~~~
Base configuraion on router
R1(config)#int f0/0
R1(config-if)#ip add 10.1.12.1 255.255.255.252
R1(config-if)#no shut
R1(config-if)#int f0/1
R1(config-if)#ip add 11.11.11.1 255.255.255.0
R1(config-if)#no shut
R1(config-if)#int lo 0
R1(config-if)#ip add 1.1.1.1 255.255.255.255
~~~
**Bring up eBGP neighborship**
~~~
R1
R1(config-if)#ip route 2.2.2.2 255.255.255.255 10.1.12.2
R1(config)#router bgp 64500
R1(config-router)#neighbor 2.2.2.2 remote-as 64510
R1(config-router)#neighbor 2.2.2.2 update-source lo0
R1(config-router)#neighbor 2.2.2.2 ebgp-multihop 2
~~~
Here, I will do some explanation on my command. Why we need the default route. Okay, we want to build our eBGP neighbor on loopback, we do this for a reason that we dont want to see physical failure affect our beautiful bgp connect. But how do we reach loopback interface. **Here, we can just write a default route**. Do not forget multi-hop cuz we need two steps to reach loopback 0.

**BGP neighbor state**
- Idle: down state
- Connect: try for tcp connection
- Active: tcp connection has been acheived
- OpenSent: tcp connection exists and a BGP Open message sent to the peer
- OpenConfirm: Open message sent and received
- Established: This is a happy state

**Inject route into BGP**

We can totally inject routes using `network` command or `redistribute` static command. 
~~~
R1(config)#ip route 11.11.0.0 255.255.0.0 null 0
R1(config)#router bgp 64500
R1(config-router)#redistribute static route-map RDtoBGP
R1(config)#route-map RDtoBGP permit    
R1(config-route-map)#match ip address STATIC
R1(config-route-map)#description Because I may have multiple static routes in routing table of R1, I only select 11.11.0.0 to null0 route.
% Description too long. Truncated to 100 characters.
R1(config)#ip access-list standard STATIC
R1(config-std-nacl)#permit 11.11.0.0 0.0.255.255
R1(config-std-nacl)#exit
~~~ 
**Internal BGP Configuration**

We can see that if we `show ip route bgp`, R4 can only have route of 23.23.23.0 cause in last step, I advertise the route with the network command.

Then, how can we make R4 reach the network of 11.11.0.0/16. Here, we also need to consider Next-hop reachability issue iBGP doesn't change next-hop address. When R2 learns about 11.11.0.0/24 from R1, it knows that the next-hop to reach 11.11.0.0/24 is R1. When in iBGP R2 wants to advertise the network to R3, it doesn't update the next-hop to itself (R2) it teachs the R3 about 11.11.0.0/24 but with the R1's address as the next-hop which R3 doesn't know how to reach to. So there are 2 solutions:

- Let R3 know how to reach R1
- Update the route for R3 in R2
~~~
R2(config)#router ospf 1
R2(config-router)#network 23.23.23.2 0.0.0.0 area 0
R2(config-router)#network 2.2.2.2 0.0.0.0 area 0  
R2(config)#router bgp 64510
R2(config-router)#neighbor 3.3.3.3 remote-as 64510
R2(config-router)#neighbor 3.3.3.3 update-source loopback 0
R2(config-router)#neighbor 3.3.3.3 next-hop-self
~~~

It is obviously that we build the iBGP with our lovely ospf, we network the 2.2.2.2 instead of writing another default route.






