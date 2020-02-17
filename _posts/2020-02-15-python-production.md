---
layout: post
title: Writing Production-grade Python Code
---

My thoughts on Git, in other word, vision control, we can have a roll back.  

~~~
git diff 
#handy to see the uncommited change, appending update. green is added while red is deleted.
git checkout -- .
##so we can roll back with this command 
~~~
**Some ideas for Error Checking**

We can assure valid CLI arguments and check File I/O.
<img src="/img/posts/sys_argc.png" alt="error-checking" align="center"/>
~~~
#pre error-checking
if len(sys.argv) != 2:
    print(f"usage: python {sys.argv[0]} <file_to_uplaod>")
    sys.exit(1)
if not os.path.isfile(sys.argv[1]):
    print(f"error: file '{sys.argv[1]}' not found")
    sys.exit(2)     
main(sys.argv)
~~~
Beautification with Formatters. We need eliminate "snowflake" code and make sure inter-project consistency.

**Demostration**
~~~
black filesafe_netmiko.py 
~~~
Bug checking with Linters. We can use it to find syntax and styling issues. 
