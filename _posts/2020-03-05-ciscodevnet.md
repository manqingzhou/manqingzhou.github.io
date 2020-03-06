---
layout: post
title: Introduction with CiscoDevNet
---
It is going to be a pretty messy post since I never studied this stuff before. So, I would not have a general idea what it is. Let's just dive into it.

This is an example Python script that runs TDR test for every interface in a up status. The output is thtown to screen, plus written to a file in bootflash.
~~~
# importing the cli module is necessary to run
import cli
#we r pacing some of the execution
import time
#we use the cli.execute API and simple matching to get a list of what we want
o1 = cli.execute('show ip int brief | include Ethernet1/0/.*up');


intfs = dict()
def grab_intf(i):
    global intfs
    if i == "":
       return
    j = (i.split(''))[0]#take the first column of space separated data
    intfs[j] = "" #assign the interface name as a key value
for i in o1.split('\n'): #apparently split it on each line.
    grab_intf(i)
#so the reason we generate a dic is to store the name of interface, why not use # a empty []
for i in intfs: #by far i believe its a dic with only key value for now
    cmd = "test cable-diagnostics tdr interface " + i
    o2 = cli.execute(cmd);
#next, we r getting data for our interface.
done = False
while done == False:
      for i in intfs:
         if intfs[i] != "":
           continue #here,if its not empty,okay we go back to for loop.
         cmd = "show cable-diagnostics tdr interface " + i 
         o2 = cli.execute(cmd);
         if "Not Completed" in o2:
             continue
         else:
            intfs[i] = o2
      time.sleep(2)
      #loop again to see if we are all done, if the dic is emtpy then found_one
      found_one = False
      for i in intfs:
         if intfs[i] == "":
            found_one = True;
      if found_one == False:
         done = True
#everything is done, we now can just print output
target = open('/bootflash/myouputfile','w')
target.truncate()
for i in intfs:
    title = "Interfaces: " + i 
    print title 
    target.write(title)
    print intfs[i]
    target.write(intfs[i])
    print "\n\n"
    target.write("\n\n")

target.close()
~~~
I have to say the code is super clean and logic is pretty clear and easy to understand. What is most impressed, the code thinks about different situation, like something goes wrong, we would not put it into the dictionary.

Another example i find interesting is the slice of the log and we can get valuable information. A typical example would be log alert and send email to the administrator.
~~~
#the simple one
a = "*Apr 19 2018 18:00:07: %LINK-3-UPDOWN: Interface GigabitEthernet1/0/5, changed state to down"
arr_output = cli.cli("show log").split("\n")
for line in arr_output:
    #if we see change state to down exsit, we r gonna print it and slice line.
    a_arr = a.split("%")
    date_in_log = a_arr[0]
#print("the entry date is: %s" % (date_in_log))
    line_arr = a.split(",")
    line_arr_1 = line_arr[0].split(" ")
    str_line_arr_0 = ''.join(line_arr_1[0])
    str_line_arr_0 = str_line_arr_0[1:]
    str_line_arr_1=''.join(line_arr_1[3])  
    str_line_arr_1=str_line_arr_1[:-1]#
     log_time = time.strptime(str_line_arr_0+" "+line_arr_1[1]+" "+line_arr_1[2]+" "+str_line_arr_1, "%b %d %Y %H:%M:%S") 
#we r gonna compare mktime(log_time) and currtime. If delta is less than 5 minutes, that log would be counted.
~~~

