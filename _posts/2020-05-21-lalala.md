---
title: Cyber Threat
subtitle: Static analysis vs Dynamic analysis, IR, DGA, Snort, Hex, Http status
layout: post
---
Recenly, I passed an online test about basics of Incident Response test. It has four parts: developer, network, attack and linux. I have to say, none of it is easy, and the test really focuses on the up-to-date techniques. The terrible thing is that I forgot to take a photo of the test and I set my google search history `private`. I lost all records of the test and now I need to study in general.

In this article, I am gonna touch on some content I still remember from the test, it has all the basics you need to know about being a cyber security analyst. 

**Static Analysis versus Dynamic Analysis**

Static analysis is always performed by a person who would review the code to ensure proper coding standards. They would look for
- proper nesting
- numbers of function calls
- comment frequency
- lines of code

The benefit of it is to find issues with the code before its ready for integrationg and further testing. 

Dynamic Analysis is based on the `system execution`, often using tools. It would identify vulnerabilities in a runtime environment. Wait a second, it is for the QA? It seems a little off to me....

But anyway, the main idea is the same that staic would not run the program but purely check the source code using automated tools. 

**Snort**
