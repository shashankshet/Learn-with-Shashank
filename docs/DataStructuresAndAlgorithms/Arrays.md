# Arrays and strings

1. LeetCode 88: Merge Sorted Array step by step.

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
🧪 Example Walkthrough:
Input:

ini
Copy
Edit
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6], n = 3
Steps:

Start with p1 = 2, p2 = 2, p = 5

Compare 3 and 6: place 6 at nums1[5]

Compare 3 and 5: place 5 at nums1[4]

Compare 3 and 2: place 3 at nums1[3]

Compare 2 and 2: place 2 at nums1[2]

Copy 2 from nums2[0] to nums1[1]

Final result: [1,2,2,3,5,6]

