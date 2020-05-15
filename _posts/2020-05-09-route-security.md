---
title: Fundamental Router Security Concepts
layout: post
---
There are several subjects in this topic.`Access Control Lists`, `Mnagement Plane Security`.

Here are a detailed list of router security policy:
- Password
- Authentication: local database or external AAA server,
- Access: SSH? HTTPS? Telnet? 
- Services: Enabled services or should it be disabled
- Redundancy: If a router fails, is there a backup router to take over?
- Routing protocols: Authentication used for routing protocol.

**Access Control Lists**

Standard ACLs could match traffic based on source IP addresses and how extended ACLs could match traffic based source, destination ip address and a variety of other criteria such as port numbers.

Here are some examples we can use to utilize this protocol starting with **ip access-list extended INFRASTRUCTURE**
!BLOCK PACKET FRAGMENT
~~~
deny   tcp any any fragments
deny   udp any any fragments
deny   icmp any any fragments
deny   ip any any fragments
~~~
!ALLOW NECESSARY ROUTING PROTOCOL
~~~
permit tcp <address-of-management-stations> any eq 22/161(SSH/SNMP)
permit icmp <address-of-management-stations> any echo
~~~
!DENY ALL OTHER TRAFFIC OR PERMIT ANY TRAFFIC
~~~
deny   ip any <address-space-of-internal-network>(deny outside ip for inside)
permit ip any any
~~~
Last step, we should always apply it to the interface
~~~
interface Serial1/0
ip access-group INFRASTRUCTURE in
~~~

**Secure Shell Versus Telnet**

The issue with Telnet is that it sends data across a network in clear text. okay, lets give it a shot on GNS3.

****
