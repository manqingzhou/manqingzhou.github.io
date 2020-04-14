---
layout: post
title: Troubleshooting with Wireshark
subtitle: Identify the issue from different protocols
---
Network services are fundenmental to the network (DHCP,DNS,NAT). Just type the protocol you want to analyze in the filter like icmp

Seperate issue in its layer and pinpoint it. Wireshark arp protocol and see one simple ip address have multiple mac adress, you should be aware of arp posioning. Next, if you see a ip address sends out tons of arp request, keep in mind it may be someone want to dig in the network and pass some virus later. When we send a arp request, it is usually broadcast until we have it in our arp cache, then it is unicast. Remember in a interview, I was talking about how a client reaches to the internet, I was describing dns resolution (may have some dhcp discovery),tcp three-way handshake, http get/post. The person reminds me of default gateway. I was like, yeah, it should be reachable, ha! I totally forget we need to arp the mac address of that default gateway since its inside layer2. 

Next, I am touch on a little bit of ip header. Little did I know people would ask questions about this. Ip header we have Flags to tell us if we need to fragement. Here, we should always remember the MTU. We also have protocol to use. Time to live to check how many routers and switches we need to pass. 

For example, we have a ip with 1500bytes with MTU 1400bytes. We definitely need to fragment that data into 100 and 1400 bytes. Sometime, we deicide not break up the messages sometimes. 

What about identification number, its unique for every packet. So we can if the pc is randomizing tis number. If the number is jumping pretty big, we can see that the server is also talking to different clients.

We can definitely if the packet is fragmented or not by seeing More fragment: set. The first offset is always 0. If dont fragment is set, then we dont break down the packet.

Next, ICMP protocol, it is used for no more than ping message. we often use it fon troubleshooting issues. This reminds me of a small troubleshooting scenario that why we cannot ping default gateway, maybe its not in the same network or the interface is not up. 

In the last section, lets dig right into UDP which does not require a connection, just src/des port, we use that for time senstive applications. No priority or identification. We can just see source port, destination port, checksum and length. DNS(53) and SNMP is using UDP. When we send a snmp requsest and see destination unreachable. Maybe SNMP agent is not supported. 

To understand dynamic host configuration protocol. Thats lot of information in it. DHCP is a dynamic way to assign ip address. The client would send a DHCP discovery, this packet is broadcasted, we can also request subnet, dns server and default gateway. The server offers something and client sends a request of which ip address it wants. The session ends with ACK. Sometimes, the pc would do some validations to make sure its not duplicate(arp request). 

Sometimes we configure dhcp relay on router.(I believe the name is helper)

Okay, this is a real ending section with FTP, HTTPS and SSL.

File Transfer Protocol is used to move files inside network. Works on port 21. 

We also need to troubleshoot some tcp issues.lool. My brain is officially drained.
 
