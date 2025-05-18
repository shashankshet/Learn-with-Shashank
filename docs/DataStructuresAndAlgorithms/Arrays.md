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