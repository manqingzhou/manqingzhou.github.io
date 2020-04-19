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

