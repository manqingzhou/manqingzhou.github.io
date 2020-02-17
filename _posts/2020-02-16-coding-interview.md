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

**Count and Say**
~~~
1. 1
2. 11
3. 21
4. 1211
5. 111221
~~~
The main problem is to calcuate the last sequence and count them. For example, we can count #4 as one 1, one 2 and two 1, which is #5,111221.

**Two sum**
a = [2,7,9,11] target = 9, the moment we make hashtable, we also compare next one with our content, key is num and value is the index as the question ask it.
~~~
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        h = {}
        for i, num in enumerate(nums):
            n = target - num
            if n not in h:
                h[num] = i
            else:
                return [h[n], i]
~~~
**Valid Palindrome**
~~~
Input: "A man, a plan, a canal: Panama"
Output: true
~~~
We can acutally slove the problem with two pointers instead of using the python function reversed. Also, the comman question of using two pointers is that when we move the pointer, dont forget to i is always smaller than j.
~~~
class Solution:
    def isPalindrome(self, s: str) -> bool:
    #this is not my solution, but i like two pointers    
        i = 0
        j = len(s) - 1
        s = s.lower()
        while i < j:
            while i < j and not s[i].isalnum():
                i += 1
            while i < j and not s[j].isalnum():
                j -= 1
            if s[i].isalnum() and s[j].isalnum() and s[i] != s[j]:
                return False
            i += 1
            j -= 1
        return True
~~~
**Reverse words in a String**

                
