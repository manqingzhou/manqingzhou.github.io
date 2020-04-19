---
layout: post
title: Summary for Another Interview
---
It is been three days since I finished my last interview. In general, the interview is not bad, the topic goes deep into ccnp study. It has the real-time troubleshooting with the manager. He draw the scenario and gave me some questions and I needed to figure out where it went wrong. I dont remember the specific detail, but the router on the stick really got me. I decide to regenerate the configuration in GNS3.

Before we go deeper, I created a small and easy task for me to sooth my way into making deeper configuration.

<img src="/img/posts/experiment1.png" alt="small task" align="center/">

I used the router c3725 and layer 2 switch. The configuration is super simple
~~~
R1
two interface plus a default route 
ip route 0.0.0.0 0.0.0.0 10.0.0.2
~~~
~~~
pc
ip 192.168.1.100 255.255.255.0 192.168.1.1
~~~
In the end, you can show ip route on router 1 and be able to ping pc. You can see three connected routes and one default route on route 1.

Okay, lets dig into router on a stick or router on the stick. The case would be a router, a layer2 switch and two pcs on different vlans. What we need to configure? Next scenario I would be configuring the ipsec vpn and explain the concept o it.

The whole enviroment is based on GNS3 VM, we eould need router c3725, layer2 switch and two pcs as I mentioned before. The topology can be shown down below:
<img src="/img/posts/vlan_routing.png" alt="router on a stick" align="center/">

Same configuration on pc, ip address + subnet mask + default gateway

Configuration on layer2 switch
~~~
vlan 22
vlan 33
int g0/0
switchport trunk en dot1q
switchport mode trunk
switchport trunk allow vlan22,33
int g0/1
switchport mode access
switchport access vlan 22
int g0/2
switchport mode access
switchport access vlan 33
~~~
When I finished the configuration, I use show vlan brief and show int g0/0 switchport
Configuraion on Router
~~~
int f0/0
no ip address
no shut down
int f0/0.22|f0/0.33
encapsulation dot1q {vlan id}
ip add 10.xx.0.1 255.255.255.128
~~~
In order to validate the configuration on router, definitely need to check show vlans and show ip route.


