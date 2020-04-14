---
layout: post
title: Some Network Details You May Ignore
subtitle: Cybersecurity Included
---

Recently, I have been staying home and studying for my interview. No matter how well I prepare, there are always something I don't know. It is super frustrating and anywho, I decide to write it down to keep my memory fresh.

The first question is what is OSI model. Super basic, nothing to address. Next, what is port mirroring. For those who don't know (including me), it is used for packet capture for some network troubleshooting. Normally, switch would not broadcast packet to all the ports. It would check it CAM table and forward the packet. So, how can we know the traffic if that's case. Well, port mirroring is the thing.

Speaking of layer 2, there is this scenario, you wireshark the packet and you see one ip address with different mac-address. Congratuation, it is ARP poisoning.In normal case, ip2 should be binding with macB. The attacker will send the arp reply with ip2 with macC. As a result, the packet will be forwarded to the attacker. 

Any questions you can think of layer 2? layer 2 should be in the same network,lool. There are some technology you should be know about switch like vlan, trunk.
Why you need know trunk cuz you need different vlan trunk traffic to pass. oh! stp, spanning tree protocol to avoid the broadcast storm of the redundancy of two or multiple switches.

Now, let's get to layer 3. How could you not know the UDP header...Just source port and destination port (plus checksum and length). OKAY, the header the TCP is complicated. We have source port and destination port, sequencing number, ack number,checksum. You know what you are missing. The fucking tcp flag!!! URG,SYN,ACK,RST,FIN,PSH.

Another thing you need to know about is tcp and udp, which protocol uses udp(tftp,snmp,dns). Some poeple may ignore it,lool. Also, what is a snmp server, explain it in detail. The classic ip range??? The difference between pop3 and smtp server.

SMTP is used to the send the email fromt the client to the server while POP3 is used to retrieve email from the server and then delete that email from the server, safe huh?

I dont know there are so many information I dont know, please tell me what is the syslog server, it is used to keep track of the log information.

We also need to know the difference between stateful and stateless firewall. Static NAT and PAT. VPN, ipsec vpn, ssl vpn and dmvpn. You should the detail of them for sure. Like authentication, encryption and hashing. Then I was asked to lise some encryption ways. I also talked about ransomware. Then, I also need to know AAA??? Authentication, authorization and accouting.

Some other basics like DHCP, DNS, SNMP, OSPF, BGP. Basic commands on linux and pc. Some easy troubleshooting,loool. HMMMMM. what else, anti-spam and ids/ips. I highlg suggest if you want to know what poeple are doing. Really check the job decription and employee on linkedin. 

That's just what I remember, if anything else i did not mention, check glassdor for the job.People are definitely willing to share with you. 

IT IS A ROUGH PATCH FOR EVEYONE LOOKING FOR A JOB. BUT DONT EVER GIVE UP!!!
