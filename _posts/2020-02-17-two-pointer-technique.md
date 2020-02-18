---
layout: post
title: Two-pointer Technique
---
When I am preparing my technical interview, I see the importance of array(with strings inside). 
**Remove Duplicate without using extra space**

This is a tricky question because we should definitely not gonna remove any number from the array
~~~
[0,1,1,1,2,3,4,5] ---> [0,1,2,3,4,5],length=6 which start+1
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        start = 0
     
        for end in range(1, len(nums)):
            if nums[start] != nums[end]:
                start +=1
                nums[start] = nums[end]
            
        return  start + 1
~~~
~~~
remove elements
[3,2,2,3]-> [2,2] remove the val 3
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        start = 0
    
        for end in range(len(nums)):
            if nums[end] != val:
                nums[start] = nums[end]
                start += 1
                
            return start
~~~
**Rotate Array**
~~~
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
~~~
~~~
class Solution:

        #the idea would be reverse the whole array and reverse the first k steps and then the rest of them
    def reverse(self, nums: List[int], left: int, right: int) -> None:
        while left < right:
             nums[left], nums[right] = nums[right], nums[left]
             left, right = left + 1, right - 1
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        
        """
        k = k % len(nums)
        self.reverse(nums, 0, len(nums) - 1)
        self.reverse(nums, 0, k - 1)
        self.reverse(nums, k , len(nums) -1 )
~~~
Next question we used to use hashtable to solve the question, but now I think two pointer is another good one.
~~~
Two sum || when the input array is Sorted
Numbers = [2,7,11,15], target = 9
output: [1,2] based on the index
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        start = 0
        end = len(numbers) - 1
        while start < end:
            s = numbers[start] + numbers[end]
            if s > target:
                end -= 1
            elif s < target:
                start += 1
            else:
                return start + 1, end + 1
~~~
~~~
The classic container with mose water solution
class Solution:
    def maxArea(self, height: List[int]) -> int:
        #this technique would be using two pointers, and we always wanna move the shorter one, cuz otherwise we would be limited by it. Also, it is definitely the first try to solve maximum question
        start = 0
        end = len(height) - 1
        max_container = 0
        while start < end:
            max_container = max(max_container,min(height[start],height[end])*(end-start))
            if height[start] < height[end]:
            
                start += 1
                
            else:
           
                end -= 1
               
       
        return max_container
~~~
Next would be medium level question Product of Array Except Self
~~~
Input:  [1,2,3,4]
Output: [24,12,8,6]
class Solution:        
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        #we can think it of product of two lists
        length = len(nums)
        L,R,output = [0]* length, [0]* length, [0]* length
        L[0] = 1
        for i in range(1,len(nums)):
            L[i] = L[i-1] * nums[i-1]
        #self.reverse(nums,0,len(nums)-1)
        R[length -1 ] = 1
        for j in reversed(range(len(nums)-1)):
            R[j] = nums[j+1] * R[j+1]
            
        for number in range(len(nums)):
            output[number] = L[number] * R[number]
        return output
~~~        
