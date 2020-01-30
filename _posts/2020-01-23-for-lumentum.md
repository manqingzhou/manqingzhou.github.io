---
layout: post
title: Preparation For Network Engineer Interview
subtitle: Technical Interview
---
My potential duties would be support routine operations and problem resolution of network related issues containing the following stuff.

- LAN(PoE,STP,EIGRP,HSRP,VLAN)
- WAN(BGP,PBR,MPLS)
- Firewalls&VPNs

The other job I may need to do is assist in the design and implementation of cloud, monitor and support networking protocols including Cloud infrastructures(DHCP, DNS, switching, routing). In the end, the job requires the management of the network capacity through network utilization, Qos, IP allocation, port density.

That is what the job wants you to know, but as the basics of network engineer, I would say you better know OSI and TCP/IP models(HOW CAN YOU NOT KNOW TCP AND UDP???).

Okay, let me talk about those protocols in details. OSI(Open Systems Interconnection) models, the goal of which is to isolate the functions of a networking system. There are seven layers, Layer 1-Physical, Layer 2-Data Link, Layer 3-Network, Layer 4-Transport, Layer 5-Session, Layer 6-Presentation, Layer 7-Application.This is actually helping to narrow down problems(Is it a physcial issue or something wrong with the application). 

Let me decribe it in details, application, for sure, the app we see in daily life such as Skype, Outlook or Google Chrome. Layer 6 is used for presentation, it decides how we show the data. A good example of it would be encryption and decryption of data for secure transimission. 

Layer 5 is when two devices wanna talk, lets set up a session for those buddies.It involves setup, coordination and termination. Speaking of layer 4, it has some important protocols TCP as well as UDP, I will talk about them later. You will know their function is to decide how much data, at what rate, where it goes.

Layer 3 is the most important one I assume. It is responsible for packet fowarding like routing through different routers.

**Next question you need to know is what is TCP/IP**

It is another network model having only four layers like Application, Transport, Network and Physical.

Or we call it Transmission Control Protocol/Internet Protocol. It is used for connect network devices on the internet. TCP, It controls how a messages is broken into smaller packets and re-assmeble in the right order at the destination. IP is just used to make sure when we route the packets, it goes to the right place/destination. 

Also, I need to address the model in detail, the application layer is just some application protocols such as HTTP, FTP, SMTP While the transport layer is just maintaining end-to-end communications aross the network. TCP handles communications between hosts and provides flow control and reliability. UDP doesnt care about building sessions like Three handshake, its job is like, we need to transmit this data as fast as possblle, usually for video conferencing,VoIP data. Keep this in mind. If reliability is the priority, TCP is the best option. If performance is the primary concern, UDP might be the answer. The network layer deals with packets and connect independent networks to transport the packets. It has IP and ICMP(USED FOR ERROR REPORTING).

**Local area network**

PoE(Power over Ethernet), it is made to let network cables carry electrical power. For exmaple, for a device such as camera in campus, it would need network connection and power connection, with PoE, only network connection needs to be made.

Next, you need consider the budget, what kind of switch u wanna buy, do you really need those 10Gb switches. Also, dont forget to buy the same device for maintance reasons and install network management tools to keep an eye on switches and routers.

**What is bridge and switch**

I am not sure if any company still use brige, but i know how it works, it is used to connect two LANs, it would broadcast every single message to all possible destinations and cause unnecessary traffic. Thats the reason we assigns address to nodes so that packets can only forwarded in one direction.

Switch is a device for sending a packet to its next destination. The trip from one switch point to another in the network is called a hop.
<img src="/img/posts/bridge and switch.png" alt="difference" align="center"/>
You can see, switch connects multiple clients to one network. 
Besides, i want to mention hub here, it sure relay message to all ports in the hub.

Switch can also break up a single LAN into mutiple VLANs. Each VLAN has its own ip subnet. Device in the same VLAN and IP subnet can communicate at Layer 2. But if one device is in VLAN 10 and the other one is in VLAN 20, then they probably need a router. So when we configure switch, we only need to write down, vlan <range or id>, name of the vlan, switchport mode, switchport access vlan.

Why we need vlan, it is for isolation. Imagine, in the comapny, we have different departments such as finance, engineer, product team. We dont want them in the same network for some safety reasons.

Okay, since we are talking about switches and vlans. There is something we need to consider, what if we have too many vlans, it would cause **broadcast storm**,

That is why we use Spanning Tree Protocol(STP) to block redundant physical linksamong switches to prevent loops. This protocol will determine a single path.

**What is HSRP and VRRP**
Hot Standby Router Protocol is a Cisco protocol which allows mutiple client gateways as one 'virtual' router. From the perspective of client, I see one gateway, i send my packet there, this protocol would then choose an active router, even active router fails, standup one can take the job and forward the packets.
<img src="/img/posts/HSRP.png" align="hot standby router protocol" alt="center"/>
As you see, two routers share one virtual ip address, and their real ip address are not shown to the client.
**What are OSPF, BGP, EIGRP**
 

**Subnetting**
**What is NAT/PAT**
**Differences between routers and switches?**
**How does BGP work**


