# Arrays and strings

**LeetCode 88: Merge Sorted Array step by step.**

🧠 Problem Understanding:
You're given:
Two sorted arrays nums1 and nums2.
nums1 has extra space at the end to hold all elements from nums2.
The actual number of meaningful elements in nums1 is m.
The number of elements in nums2 is n.

Your task is to merge nums2 into nums1 in-place, so that nums1 becomes a fully sorted array.

🔍 Key Insight:
Since nums1 has extra space at the end, we can fill from the back instead of the front. That way, we don’t overwrite any elements we haven’t checked yet.

✅ Strategy:
Use three pointers:
p1 = m - 1: points to the last element in the actual nums1 values.
p2 = n - 1: points to the last element in nums2.
p = m + n - 1: points to the last position in nums1.

Compare elements from the back of nums1 and nums2, and place the larger one at position p.
Decrease p and whichever pointer (p1 or p2) you just used.
At the end, if any elements are left in nums2, copy them (this only happens if they are all smaller than nums1's smallest).

🧑‍💻 Code (Python):
```

def merge(nums1, m, nums2, n):
    p1 = m - 1  # last element of nums1 (non-zero part)
    p2 = n - 1  # last element of nums2
    p = m + n - 1  # last position in nums1

    # Compare from the end
    while p1 >= 0 and p2 >= 0:
        if nums1[p1] > nums2[p2]:
            nums1[p] = nums1[p1]
            p1 -= 1
        else:
            nums1[p] = nums2[p2]
            p2 -= 1
        p -= 1

    # If any elements are left in nums2
    while p2 >= 0:
        nums1[p] = nums2[p2]
        p2 -= 1
        p -= 1
```

**LeetCode 27: Remove Element.**

🧠 Problem Understanding
You are given:

An integer array nums
An integer val

Your task:
Remove all instances of val from the array nums, in-place
Return the count of elements that are not equal to val

🔸 Constraints:

You don’t need to maintain the order of elements
Do it in-place (no extra space)

✅ What You Need to Do:
Modify nums in-place such that:
The first k elements are the ones not equal to val
Return k, the number of elements not equal to val
⚠️ The contents beyond the first k elements don't matter.

🔍 Strategy (Two Pointer Approach):
Use a write pointer (i) that keeps track of where to write the next non-val element.

Steps:
Initialize i = 0
Loop through each element num in nums
If num != val:
Write num at index i → nums[i] = num
Increment i
At the end:
First i elements of nums are the result
Return i

🧑‍💻 Python Code:
```
def removeElement(nums, val):
    i = 0  # write pointer

    for num in nums:
        if num != val:
            nums[i] = num
            i += 1

    return i
```
**LeetCode 26: Remove Duplicates from Sorted Array.**

🧠 Problem Summary:
Given:
A sorted integer array nums (non-decreasing order).

Your task:
Remove duplicates in-place such that each unique element appears only once.
Keep the relative order of the elements the same.
Return the count k of unique elements.
The first k elements in nums should be the unique values in order.

🔍 Key Insight:
Because the array is already sorted, all duplicates will be next to each other.
We can use the two-pointer technique:
One pointer (i) keeps track of the last unique element
Another pointer (j) scans through the array

✅ Strategy (Two Pointers):
If the array is empty, return 0.
Start with i = 0 (position to write next unique value).
Loop j from 1 to end of the array:
If nums[j] != nums[i], it means a new unique element is found.
Move i one step ahead
Copy nums[j] to nums[i]
At the end, return i + 1 (count of unique elements)


```

def removeDuplicates(nums):
    if not nums:
        return 0

    i = 0  # pointer to last unique element

    for j in range(1, len(nums)):
        if nums[j] != nums[i]:
            i += 1
            nums[i] = nums[j]  # place unique element at the correct spot

    return i + 1
```

**Remove Duplicates from Sorted Array" problem — this is sometimes referred to as “Remove Duplicates II” on LeetCode.**

🧠 Problem Summary:
Given:

A sorted array nums (non-decreasing order).
Your task:
Modify the array in-place so that each unique element appears at most twice.
Keep the relative order the same.
Return k, the number of valid elements in the modified array (first k elements).

🔍 Key Idea:
Since the array is sorted:
All duplicates are grouped together.
You are allowed up to 2 of each element.
We’ll use the two-pointer technique again:
Pointer i is the write pointer (where to write the next valid element).
Pointer j scans through the array.

✅ Strategy (Two Pointers with a Rule):
Initialize i = 0 (start writing from the beginning).
Loop through the array with j:
If i < 2, always write nums[j] (first two elements are always allowed).
If nums[j] != nums[i - 2], then write nums[j] at nums[i].
Why i - 2? Because we’re allowing at most 2 of the same number.

🧑‍💻 Python Code:
```
def removeDuplicates(nums):
    i = 0  # write pointer

    for num in nums:
        if i < 2 or num != nums[i - 2]:
            nums[i] = num
            i += 1

    return i
```


**Given an integer array nums, return the majority element — the element that appears more than n//2 times.
You are guaranteed that a solution always exists.**

🧠 Your Code:
python
```
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        counts = {}
        max_count = len(nums)//2

        for num in nums:
            if num in counts:
                counts[num] += 1
            else:
                counts[num] = 1

            if counts[num] > max_count:
                return num
```
🔍 Explanation:
Step 1: Initialize dictionary and threshold
python
Copy
Edit
counts = {}
max_count = len(nums) // 2
counts is a dictionary to store the frequency of each number.

max_count is the majority threshold. A number must appear more than this to be considered the majority element.

Step 2: Loop through each number
python
Copy
Edit
for num in nums:
Iterate through each element in the nums array.

Step 3: Count frequency of each number
python
Copy
Edit
if num in counts:
    counts[num] += 1
else:
    counts[num] = 1
If the number already exists in the dictionary, increment its count.

Otherwise, initialize its count to 1.

Step 4: Check if it's the majority
python
if counts[num] > max_count:
    return num
After updating the count, check if it crossed the majority threshold.

If yes, return it immediately (early exit — very efficient).

**Leetcode 189. Rotate Array step-by-step so you fully understand it.**
✅ Optimal Approach (O(n) Time, O(1) Space):
We can solve this in 3 simple steps using array reversals:

🔁 Key Idea:
To rotate right by k:

Reverse the whole array

Reverse the first k elements

Reverse the remaining (n-k) elements

👇 Example Walkthrough:
python
Copy
Edit
nums = [1,2,3,4,5,6,7]
k = 3

 Step 1: Reverse all → [7,6,5,4,3,2,1]
 Step 2: Reverse first 3 → [5,6,7,4,3,2,1]
 Step 3: Reverse rest → [5,6,7,1,2,3,4]
Done!

✅ Python Code:
python
```
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        n = len(nums)
        k %= n  # handle k > n

        def reverse(start, end):
            while start < end:
                nums[start], nums[end] = nums[end], nums[start]
                start += 1
                end -= 1

        # Step 1: Reverse the whole array
        reverse(0, n - 1)

        # Step 2: Reverse first k elements
        reverse(0, k - 1)

        # Step 3: Reverse remaining n-k elements
        reverse(k, n - 1)
```
✅ Time & Space Complexity:
Time: O(n)

Space: O(1) (in-place)

***Leetcode 121: Best Time to Buy and Sell Stoc***
✅ Optimal Solution (O(n) Time, O(1) Space):
🎯 Key Idea:
Track the lowest price so far (best day to buy).

At each day, calculate the potential profit if we sold on that day.
Keep updating the maximum profit.

👇 Step-by-Step Walkthrough:
python

prices = [7,1,5,3,6,4]

min_price = ∞
max_profit = 0

Day 0: price = 7 → min_price = 7
Day 1: price = 1 → min_price = 1
Day 2: price = 5 → profit = 5 - 1 = 4 → max_profit = 4
Day 3: price = 3 → profit = 3 - 1 = 2 → max_profit = 4
Day 4: price = 6 → profit = 6 - 1 = 5 → max_profit = 5 ✅
Day 5: price = 4 → profit = 4 - 1 = 3 → max_profit = 5

✅ Python Code:
python
```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_price = float('inf')  # Start with a very high price
        max_profit = 0

        for price in prices:
            if price < min_price:
                min_price = price  # Update the lowest price so far
            elif price - min_price > max_profit:
                max_profit = price - min_price  # Update max profit if better

        return max_profit
```
✅ Time & Space Complexity:
Time: O(n) → We loop through the prices only once.

Space: O(1) → No extra space used.


***Leetcode 122. Best Time to Buy and Sell Stock II***

🧠 Problem Summary
You are given a list of stock prices, where prices[i] is the price on day i.
You can buy and sell as many times as you want (even on the same day), but you must sell before you buy again (you can't hold more than one share at a time).

Goal: Maximize your profit.

✅ Key Insight
This problem is about taking every opportunity to make profit, no matter how small.
👉 If the price tomorrow is higher than today, then buy today and sell tomorrow.
For example:

plaintext

prices = [7,1,5,3,6,4]
          ↑ ↓ ↑ ↓ ↑ ↓
Opportunities to make profit:

Buy at 1, sell at 5 → profit = 4
Buy at 3, sell at 6 → profit = 3
Total profit = 4 + 3 = 7

💡 Greedy Approach (Simple)
python
```
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = 0
        
        for i in range(1, len(prices)):
            if prices[i] > prices[i - 1]:
                profit += prices[i] - prices[i - 1]
        
        return profit
```
🧪 Explanation
We loop from day 1 to end.

If today’s price (prices[i]) is greater than yesterday’s price (prices[i - 1]), it means we could’ve bought yesterday and sold today.
So, we add the profit: prices[i] - prices[i - 1].
This effectively adds up all positive profit differences — which is exactly what we want.

⏱️ Time and Space Complexity
Time: O(n) — One pass through the list.

Space: O(1) — Constant space used.

***LeetCode 55 – Jump Game.***
Greedy Observation
While scanning from left to right, it is enough to know the furthest position we can reach so far.

Why?
Suppose we are at index i.
If the current furthest reachable index (far) is ≥ i, we have already proven we can stand on i.
From i, the best we can do is extend far to max(far, i + nums[i]).

If at any time far < i, we hit a “gap” we cannot cross → return false immediately.

If we finish the scan with far ≥ last_index, then we can reach the end → true.

This one-pass greedy works because earlier indices can only jump forward; once we’ve computed the global maximum reach up to position i, no later step can improve reachability of any earlier gap we already failed.

4 Algorithm in Plain English
python
```
far = 0                                # furthest index we can reach so far
for i from 0 to n-1:
    if i > far:                       # gap!
        return False
    far = max(far, i + nums[i])       # extend reach
return True                            # far never dropped behind i
```
Python Implementation
python
```
class Solution:
    def canJump(self, nums: list[int]) -> bool:
        far = 0
        for i, step in enumerate(nums):
            if i > far:                       # cannot even stand on i
                return False
            far = max(far, i + step)          # best we can do from here
            if far >= len(nums) - 1:          # early exit: already at/over end
                return True
        return True
```
Complexity
Value
Time	O(n) – one linear scan
Space	O(1) – just the integer far



***LeetCode 45 – Jump Game II in a way that makes it super intuitive to understand and solve.***

🧠 Problem Understanding
Given:

An array nums, where nums[i] is the maximum jump length you can take from index i.

Goal:

Reach the last index (nums[n - 1]) using the minimum number of jumps.

Constraints:

You can reach the end (i.e., it's guaranteed).

From nums[i], you can jump to any nums[i + j] where 0 < j ≤ nums[i].

🏃 Real-World Analogy
Think of it like this:

You're standing on stones in a river, and each stone tells you how many stones forward you can jump. Your goal is to cross the river in as few jumps as possible.

✅ Example
nums = [2, 3, 1, 1, 4]
Start at index 0:

You can jump to index 1 or index 2 (nums[0] = 2)

What's the best place to jump to?

Pick the one that gives you the furthest reach in the next move (greedy choice).

From index 1 (which has value 3), you can go to indices 2, 3, or 4.

So jump from 0 → 1, then 1 → 4.

Total jumps = 2

💡 Intuition
We use a greedy level-based BFS approach.
Each “jump” is like one level of BFS traversal.

Track:
currentEnd: the end of the current jump range.

farthest: the farthest index we can reach in the next jump.

Every time we reach currentEnd, we:

Increment jumps

Update currentEnd = farthest

✅ Greedy Algorithm

```
class Solution:
    def jump(self, nums: list[int]) -> int:
        jumps = 0
        currentEnd = 0
        farthest = 0

        for i in range(len(nums) - 1):  # no need to jump from last index
            farthest = max(farthest, i + nums[i])
            if i == currentEnd:
                jumps += 1
                currentEnd = farthest

        return jumps

```


 ***H-Index problem in a very simple and clear way.***

🔍 What is H-Index?
The H-Index is a number that measures both:
Productivity (number of papers), and
Impact (number of citations).

🧠 Definition:
A researcher has an index h if h of their n papers have at least h citations each, and the rest of the papers have no more than h citations.

✅ Let's break the example down:
Input: citations = [3, 0, 6, 1, 5]

This means:
Paper 1 has 3 citations
Paper 2 has 0
Paper 3 has 6
Paper 4 has 1
Paper 5 has 5

Now, we want to find the largest number h such that at least h papers have ≥ h citations.

🚀 Step-by-step Dry Run
Sort the citations in descending order:


[6, 5, 3, 1, 0]
Now go one by one and check:

At index 0: 6 citations → at least 1 paper has ≥ 1 citation ✅

At index 1: 5 citations → at least 2 papers have ≥ 2 citations ✅

At index 2: 3 citations → at least 3 papers have ≥ 3 citations ✅

At index 3: 1 citation → at least 4 papers have ≥ 4 citations ❌ (only 3 papers do)

✅ So the highest h that satisfies the condition is 3.

✅ Final Code (Python)
```
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        citations.sort(reverse=True)
        h = 0
        for i, c in enumerate(citations):
            if c >= i + 1:
                h += 1
            else:
                break
        return h
```