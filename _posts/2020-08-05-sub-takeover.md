---
title: Hostile subdomain takeover
subtitle: Heroku/Github/Desk
layout: post
---
It is been a long time since I updated my study journey. I am officially a SOC analyst. Except from studying what I will ultilize in real life, I also want to expand my horizon by taking the perspective of attackers. Maybe I would update attack frequetly or maybe not.

Today, I am gonna focus on a non-traceable attack which is responsible for at least 17 large service providers and multiple domains. 

The team at Detectify has recently identified a serious attack vector resulting from a widespread DNS misconfiguration. This misconfiguration would allow an attack to take full control over subdomains pointing to providers such as Shoptify, Github, BitBucker, SquareSpace.
WHY IS IT DANGEROUS?

Three reasons:
- Sign up a new account and claim the domain. DONE
- The domain onwer would no know! Completely hidden
- ISP is unlikely to fix it.
Here you can verify that.
~~~
$ host x.example.com
x.example.com has address 192.30.252.153
x.example.com has address 192.30.252.154
$ whois 192.30.252.153 | grep "OrgName"
OrgName: GitHub, Inc.
~~~
omg, it is literally so easy to take over. Anyone who plays with github.io before knows that you can just custom your domain with this x.example.com

Now we have a high-level overview of what it takes to serve content on a misconfigured subdomain, now it is time to find those vulnerable ones.
[Scraping and brute forcing](https://www.hackerone.com/blog/Guide-Subdomain-Takeovers)
~~~
$ git clone https://github.com/aboul3la/Sublist3r.git
$ cd Sublist3r
$ sudo pip install -r requirements.txt
#python sublist3r.py -d hackerone.com
~~~
When brute forcing subdomains, the hacker iterates through a wordlist and based on the response can determine whether or not the host is valid. It is always helpful to check wildcard.
~~~
$ host randomifje8z193hf8jafvh7g4q79gh274.example.com
~~~
Always look for hosts containing `jira` or `git`. I would not go in deep about attacking. There are tons of resources out there teaching you how to accomplish that.

