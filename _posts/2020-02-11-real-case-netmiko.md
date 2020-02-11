---
layout: post
title: A Use Case for Network Automation
---
 
This is something I need to work on every single day. Use the Python Netmiko module to automate switches, routers and firewalls from multiple ventors. For more detail, click on [this](https://www.linuxjournal.com/content/use-case-network-automation).

SNMP could provide a lot the information we need, but it would have to be configured on each device manually first.

Most modern devices support REST APIs, but companies typically are saddled with lots of legacy devices that dont support anything fancier than Telnet and SSH. Speaking of SSH, when I was a intern, I remember using lots of ssh to get access to the device.

All the automation would be done in Python and model we use is gonna be Netmiko.It abstracts many common things you need to do when talking to switches. For example, if you run a command that produces more than one page of output, the switch CLI typically 'page' the output, waiting for input before displaying the next page. In Netmiko, all we need to do is use the `disable_paging()` function to solve the problem caused by the vendor.

**Dealing with a Mix of Vendors and Products**

Netmiko supoorts a growing list of network vendor and product combinations. Howver, we'll need to specify the information of the vendor when using the functions. For example, Cisco has several CLI versions on the different product lines, including `cisco_ios`,`cisco_nxos`,`cisco_asa`.

**A Few Words of Caution**

-Manually made a change would not cause the shutdown of the entire network devices. But network automation tools will!!!
-Configuration backup strategy: roll back to a specific "known good" point in time.
-A strategy for testing: It is possible to have a dedicated pool of representative equipment permanently set aside for testing and proof of concepts. When rolling out a change on a production network, first verify the automation on a few devices.

**Using Netmiko without Writing Any Code**

There are three tools u can use if i know, but please check the official site to see the newest update. 

`netmiko-show` would display the entire configuration.
~~~
netmiko-show --cmd "show spanning-tree detail" arista-eos | egrep "(last chage|from)"
sfo03-r1r12-sw1.txt:  Number of topology changes 2307 last
 change occurred 19:14:09 ago
sfo03-r1r12-sw1.txt:          from Ethernet1/10/2
sfo03-r1r12-sw2.txt:  Number of topology changes 6637 last
 change occurred 19:14:09 ago
sfo03-r1r12-sw2.txt:          from Ethernet1/53
~~~
This information can be very helpful when tracking down the specific switch and switch port reponsible for an STP flapping issue. `from` field gives you the source port of the change, enabling you to narrow down the source of the problem.

`netmiko-cfg`, apply snippets of configurations to one or more devices. Specify the configuration command with the `cmd`. This could be used for mass configurations including DNS servers, NTP servers, SNMP community strings or syslong servers for the entire network. For example, to configure the read-only SNMP community on all of your Arista switches:
~~~
netmiko-cfg --cmd "snmp-server community mysecret ro" arista-eos
~~~

`netmiko-grep` is used for searching for a string in the configuration of multiple devices. For example, verify the current syslog destination in the Arista switches:
~~~
netmiko-grep --use-cache "logging host" arista-eos
sfo03-r2r7-sw1.txt:logging host 10.7.1.19
sfo03-r3r14-sw1.txt:logging host 10.8.6.99
sfo03-r3r16-sw1.txt:logging host 10.8.6.99
sfo03-r4r18-sw1.txt:logging host 10.7.1.19
~~~
Dont forget all of the netmiko tools depend on an "inventory" of devices, which
is a YAML-formatted file stored in ".netmiko.yml" in the current directory or home directory.
~~~
sfo03-r1r11-sw1:
  device_type: cisco_ios
  ip: sfo03-r1r11-sw1
  username: netadmin
  password: secretpass
  port: 22
~~~
Groups for the devices type, I am not sure if its the idea of infrastructure as code. We can also indicate physical locations groups("SFO03","RKV02"), role("TOR","spine","leaf","core"),owner("Eng","QA").
~~~
cisco-ios:
  - sfo03-r1r11-sw1
cisco-nxos:
  - sfo03-r1r12-sw2
  - sfo03-r3r17-sw1
arista-eos:
  - sfo03-r1r10-sw2
  - sfo03-r6r6-sw1
~~~
Why we need groups, so we can divide our devices and use some specific commands.such as `netmiko-cfg --cmd "feature interface-vlan" cisco-nxos`. 

Also, we dont need to create a YMAL-formatted file by ourself.
~~~

sfo03-r1r11-sw1,cisco_ios
sfo03-r1r12-sw2,cisco_nxos
sfo03-r1r10-sw2,arista_eos
sfo03-r4r5-sw3,arista_eos
sfo03-r1r12-sw1,cisco_nxos
sfo03-r5r15-sw2,dell_force10
~~~
~~~
grep -v '^#' simplelist.txt | awk -F, '{printf("%s:\n
 ↪device_type:
%s\n  ip: %s\n  username: netadmin\n  password:
 ↪secretpass\n  port:
22\n",$1,$2,$1)}' >> .netmiko.yml
~~~
The final result:
~~~
sfo03-r1r11-sw1:
  device_type: cisco_ios
  ip: sfo03-r1r11-sw1
  username: netadmin
  password: secretpass
  port: 22
sfo03-r1r12-sw2:
  device_type: cisco_nxos
  ip: sfo03-r1r12-sw2
  username: netadmin
  password: secretpass
  port: 22
sfo03-r1r10-sw2:
  device_type: arista_eos
  ip: sfo03-r1r10-sw2
  username: netadmin
  password: secretpass
  port: 22
~~~

Okay, now you get the hang of the file fomrat and some tools about netmiko. The approach to the real scenario problem. The first phase was the "scanning" of the switches and storing their configurations and command output locally, the second phase was processing and seraching across the stored data.
~~~
import csv
import sys
import logging
def main():
# get data file from command line
   devfile = sys.argv[1]
# open file and extract the two fields
   with open(devfile,'rb') as devicesfile:
        fields = ['hostname','devtype']
        hosts = csv.DictReader(devicesfile, fieldnames=fields, delimiter=',')
#call host and function "login_switch()"
#for each one
   for host in hosts:
       hostname = host['hostname']
       devtype = host['devtype']
       login_switch(hostname,devtype)
~~~
Now, we need to write function login_switch to get what we want.
~~~
from netmiko import 
def login_switch(host,devicetype):
# required arguments to ConnectHandler
     device = { '': ,'':,'usrname':'admin','passwprd':'secretpass',}
     try: net_connect=ConenctHandler(**device),commands, output,path = '/root/login/scan/' + host + "/",make_dir(path), filename
     store output of command in file
     handle = open (file,'w')
     handle.write(output)
     handle.close()
~~~
**Debugging via Logging**
~~~
import logging
if _name_ == "_main_"
# logging.basicConfig(level=logging.DEBUG)
 main()
~~~
So, u can tell where things are breaking in the interaction with a network device. Maybe authentication is failed.

**Analysis Phase**

Is the hostname registered in DNS matches the hostname configured in the device.~~~
import os
import sys
directory = "/root/login/scan"
for filename in os.listdir(directory):
    prompt_file = directory + '/' + filename + '/prompt'
    try:
         prompt_fh = open(prompt_file,'rb')
    except IOError:
         "Can't open:", prompt_file
         sys.exit()

    with prompt_fh:
        prompt = prompt_fh.read()
        prompt = prompt.rstrip('#')
        if (filename != prompt):
            print 'switch DNS hostname %s != configured
             ↪hostname %s' %(filename, prompt)
~~~
Somethime its just the DNS name are not equal.
