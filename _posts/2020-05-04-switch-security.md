---
title: Switch Security
layout: post
---

For example, you should strongly consider disabling the HTTP server on a Catalyst switch. This often is used for a web-based switch-management tool but is usually unneeded in a production environment. You can disable it with the no ip http server configuration command.

Although Cisco IOS Software releases have begun to disable other uncommon services as the default, you should make sure that none of the following commands is present in your switch configuration:
~~~
service tcp-small-servers
service udp-small-servers
service finger
service config
~~~
If any of these commands are present, disable them by preceding them with the no keyword.

**Secure the switch console** In many environments, switches are locked away in wiring closets where physical security is used to keep people from connecting to the switch console. Even so, you always should configure authentication on any switch console. It is usually appropriate to use the same authentication configuration on the console as the virtual terminal (vty) lines.

**Secure virtual terminal access**. You always should configure user authentication on all of the vty lines on a switch. In addition, you should use access lists to limit the source IP addresses of potential administrative users who try to use Telnet or Secure Shell (SSH) to access a switch.

You can use a simple IP access list to permit inbound connections only from known source addresses, as in the following example:
~~~
 Switch(config)#access-list 10 permit 192.168.199.10
 Switch(config)#access-list 10 permit 192.168.201.100
 Switch(config)#line vty 0 15
 Switch(config-line)#access-class 10 in
~~~
Be sure you apply the access list to all the line vty entries in the switch configuration. Many times, the vty lines are separated into groups in the configuration. You can use the show user all command to see every possible line that can be used to access a switch.

**Use SSH whenever possible**. Although Telnet access is easy to configure and use, Telnet is not secure. Every character you type in a Telnet session is sent to and echoed from a switch in the clear, with no encryption. Therefore, it is very easy to eavesdrop on Telnet sessions to overhear usernames and passwords.

Instead, you should use SSH whenever possible. SSH uses strong encryption to secure session data. Therefore, you need a strong-encryption IOS image running on a switch before SSH can be configured and used. You should use the highest SSH version that is available on a switch. The early SSHv1 and SSHv1.5 have some weaknesses. SSHv2 is better yet but is available only in more recent IOS releases, such as 12.2(25)SEB1 on the Catalyst 3750.

**Secure SNMP access** To prevent unauthorized users from making changes to a switch configuration, you should disable any read-write SNMP access. These are commands of the form snmp-server community string RW.

Instead, you should have only read-only commands in the configuration. In addition, you should use access lists to limit the source addresses that have read-only access. Don’t depend on the SNMP community strings for security because these are passed in the clear in SNMP packets.

**Secure unused switch ports** Every unused switch port should be disabled so that unexpected users can’t connect and use them without your knowledge. You can do this with the shutdown interface configuration command.

In addition, you should configure every user port as an access port with the switchport mode access interface configuration command. Otherwise, a malicious user might connect and attempt to negotiate trunking mode on a port. You also should consider associating every unused access port with a bogus or isolated VLAN. If an unexpected user does gain access to a port, he will have access only to a VLAN that is isolated from every other resource on your network.

**Secure STP operation**. A malicious user can inject STP bridge protocol data units (BPDUs) into switch ports or VLANs, and can disrupt a stable, loop-free topology. You always should enable the BPDU guard feature so that access switch ports automatically are disabled if unexpected BPDUs are received.

**Secure the use of CDP**. By default, CDP advertisements are sent on every switch port at 60-second intervals. Although CDP is a very handy tool for discovering neighboring Cisco devices, you shouldn’t allow CDP to advertise unnecessary information about your switch to listening attackers.

CDP should be enabled only on switch ports that connect to other trusted Cisco devices. Don’t forget that CDP must be enabled on access switch ports where Cisco IP Phones are connected. When the CDP messages reach the IP Phone, they won’t be relayed on to a PC connected to the phone’s data port. You can disable CDP on a port-by-port basis with the no cdp enable interface configuration command.

