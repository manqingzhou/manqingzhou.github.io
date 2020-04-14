---
layout: post
title: Authentication
---
We need to authenticate people who want to get access to the company resource. In a physical world, it may be just a swipe card or a code to enter the locked door.

There are several ways of authentication such as password or two-factor authencations. Here I want to address that the username and password are usually stored in the local database. 

This is the first time I have ever heard the concept of server-based password authentication. The idea is to store the password on external authentication servers like LDAP, RADIUS.

Next, SSL VPN users can choose to install certificates in their web browsers to authenticate themselves. Last but not the least, we have two-factor authenticatio. In other word, we need to double check if it is a valid user.

Now, lets talk about how to utlize them in VPN, in IPsec VPN, we use pre-shared key to do this job. Remember the configuration, we have this command like preshard key plus remote gateway(vpn peer address).

For SSL VPN users, we can have username with password or user accounts authenticate by external server.

Here, I want to talk about an important server called LDAP server. LDAP directories are standard technology for storaging user, group and permission. 

It may has information of apartment, people, password, email address etc.

RADIUS(Remote Authentication and Dial-in User Service) is a client-protoc
ol that provides AAA.
