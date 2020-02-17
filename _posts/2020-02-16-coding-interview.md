---
layout: post
title: Time to prepare for on-site interview with microsoft
---
**Find ALL Anagrams in a String**
example: s: "cbaebabacd" p: "abc" output:[0,6] #It is apparently a index
~~~
#Sliding Window with HashMap
def findAnagrams(s: str,p: str):
    ns,np = len(s), len(p)
    if ns < np:
        return []
    p_count = Counter(p)
    s_count = Counter()
    output = []
    for i in range(ns):
        s_count[s[i]] +=1
        if i >= np:
            if s_count[s[i-np]] == 1:
                del s_count[s[i-np]]
            else:
                s_count[s[i-np]] -=1
        if s_count == p_count:
            output.append(i- np + 1)
    return output
~~~
One down, so many to go.
**Unique Paths**

