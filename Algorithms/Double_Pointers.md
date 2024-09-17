# 分类
双指针技巧分为2类：
- 快慢指针
> 主要解决链表中的问题，比如判定链表中是否包含环
- 左右指针
> 解决数组或字符串中的问题，比如二分查找
# 快慢指针的常见算法
## 初始化
指向头节点head
## 前进
快指针fast在前，慢指针slow在后
## 实例
1. 判定链表是否有环
```
def ahsCycle(head):
    fast=slow=head
    while not fast==Null or not fast.next==Null:
        fast=fast.next.next
        slow=slow.next

        if fast==slow:
            return True
    return False
```
2. 已知链表中含有环，返回这个环的起始位置
```
def detectCycle(head):
    fast=slow=head
    while not fastt==Null or fast.next==Null:
        fast=fast.next.next
        slow=slow.next
        if fast==slow:
            break
        
    slow=head
    while not slow==fast:
        fast=fast.next
        slow=slow.next
    return slow
```
3. 寻找链表的中点
```
def middleNode(head):
    fast=slow=head
    while fast and fast.next:
        fast=fast.next.next
        slow=slow.next
    return slow
```
# 左右指针的常见算法
## 初始化
左右指针在数组中实际是指两个索引值。  
一般初始化为left=0,right=len(nums)-1
## 实例
1. 二分查找
```
def binarySearch(nums,target):
    left=0
    right=len(nums)-1
    while left<=target:
        mid=int(right+left)/2
        if nums[mid]==target:
            return mid
        elif nums[mid]<target:
            left=mid+1
        elif nums[mid]>target:
            right=mid-1
    return -1
```
2. 两数之和
在一升序数组中找到两个数使得他们之和等于目标值
```
def twoSum(nums,target):
    left=0
    right=len(nums)-1
    while left<right:
        sum=nums[left]+nums[right]
        if sum==target:
            return [left,right]
        elif sum<target:
            left+=1
        else:
            right-=1
    return [-1,-1]
```
3. 反转数组
反转一个char数组
```
def reverseString(arr):
    left=0
    right=len(arr)-1
    while left<right:
        temp=arr[left]
        arr[left]=arr[right]
        arr[right]=temp
        left+=1
        right-=1
```
4. [Leetcode16](https://leetcode.com/problems/3sum-closest/)
```
class Solution:
    def threeSumClosest(self, target: int) -> int:
        diff = float('inf')
        nums.sort()
        for i in range(len(nums)):
            lo, hi = i + 1, len(nums) - 1
            while (lo < hi):
                sum = nums[i] + nums[lo] + nums[hi]
                if abs(target - sum) < abs(diff):
                    diff = target - sum
                if sum < target:
                    lo += 1
                else:
                    hi -= 1
            if diff == 0:
                break
        return target - diff
```
# 滑动窗口算法
## 算法框架
```
def slidingWindow(s,t):
    need=dict()
    window=dict()

    for c in t:
        need[c]=1
    
    left=right=0
    valid=0
    while right<len(s):
        #c是将移入窗口的字符
        c=s[right]
        #右移窗口
        right+=1
        #进行窗口内数据的一系列更新
        ···

        #debug输出的位置
        print("window: [%d,%d]\n",left,right)

        #判断左侧窗口是否要收缩
        while window needs shrink:
            # d是将移出窗口的字符
            d=s[left]
            # 左移窗口
            left+=1
            #进行窗口内数据的一系列更新
            ···
```
## 实例
1. 最小覆盖子串
在字符串S中找出包含字符串T所有字母的最小子串
```
def minWindow(s,t):
    need=dict()
    window=dict()
    for c in t:
        need[c]+=1
    left=right=0
    valid=0
    start=0, length=len(s)+1
    while right<len(s):
        c=s[right]
        right++
        if need.get(c):
            window[c]+=1
            if window[c]==need[c]:
                valid+=1

        #判断左侧窗口是否要收缩
        while valid=len(need):
            #更新最小覆盖子串
            if right-left<length:
                start=left
                length=right-left
            
            #将要移出窗口的字符
            d=s[left]
            left+=1
            if need.get(d):
                if window[d]==need[d]:
                    valid-=1
                window[d]-=1
    if length<len(s)+1:
        return s[start:start+length]
    else:
        return ""
```
2. 字符串排列
s是否包含t的排列
```
def minWindow(s,t):
    need=dict()
    window=dict()
    for c in t:
        need[c]+=1
    left=right=0
    valid=0
    while right<len(s):
        c=s[right]
        right++
        if need.get(c):
            window[c]+=1
            if window[c]==need[c]:
                valid+=1

        #判断左侧窗口是否要收缩
        while right-left>=len(t):
            #更新最小覆盖子串
            if valid==len(need):
                return True
            
            #将要移出窗口的字符
            d=s[left]
            left+=1
            if need.get(d):
                if window[d]==need[d]:
                    valid-=1
                window[d]-=1
    return False
```
3. 找到所有字母异位词
字母异位词指字母相同但排列不同的字符串
给定s和p，找到s中所有是p的字母异位词的子串，返回这些子串的起始索引
```
def findAnagrams(s,t):
    need=dict()
    window=dict()

    for c in t:
        need[c]=1
    
    left=right=0
    valid=0
    res=[]
    while right<len(s):
        #c是将移入窗口的字符
        c=s[right]
        #右移窗口
        right+=1
        #进行窗口内数据的一系列更新
        if need.get(c):
            window[c]+=1
            if window[c]==need[c]:
                valid+=1

        #debug输出的位置
        print("window: [%d,%d]\n",left,right)

        #判断左侧窗口是否要收缩
        while right-left>=len(t):
            if valid==len(need):
                res.append(left)
            # d是将移出窗口的字符
            d=s[left]
            # 左移窗口
            left+=1
            #进行窗口内数据的一系列更新
            if need.get(d):
                if window[d]==need[d]:
                    valid-=1
                window[d]-=1
    return res
```
4. 最长无重复子串
不含有重复字符的最长子串的长度
```
def lengthOfLongestSubstring(s):
    if len(s)<2:
        return len(s) 
    window=dict()

    right=left=0
    length=0
    while right<len(s):
        c=s[right]
        right+=1
        window[c]+=1
        while window[c]>1:
            d=s[left]
            left+=1
            window[d]-=1
        length=max(length,right-left)
    return length
```