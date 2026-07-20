# DSA Revision Notes - Arrays & Hashing

## 1. HashMap

### What is it?
A HashMap stores **Key → Value** pairs.

Example:

Age
Alice → 25
Bob → 30

Python:

```python
ages = {}
ages["Alice"] = 25
```

### Time Complexity

| Operation | Complexity |
|------------|------------|
| Insert | O(1) Average |
| Search | O(1) Average |
| Delete | O(1) Average |

Worst Case: O(n)

---

## When should I think of HashMap?

Whenever the problem mentions:

- Find two numbers
- Lookup quickly
- Mapping
- Store extra information
- Count occurrences
- Previous values
- Complement

Examples:

- Two Sum
- Subarray Sum Equals K
- Top K Frequent Elements

---

## 2. HashSet

### What is it?

Stores only unique values.

No key-value pair.

Python

```python
visited = set()
visited.add(5)
```

### Complexity

Insert → O(1)

Search → O(1)

Delete → O(1)

---

## When should I think of HashSet?

Whenever the question asks:

- Have I seen this before?
- Duplicate?
- Unique?
- Exists?
- Membership check

Examples

- Contains Duplicate
- Longest Consecutive Sequence

---

## 3. Frequency Counting

Frequency counting is simply a HashMap where:

Key = Element

Value = Count

Example

Input

a a b c a

Output

a → 3

b → 1

c → 1

Python

```python
count = {}

for x in nums:
    count[x] = count.get(x,0)+1
```

---

## Think Frequency Map when

Question asks:

- Most frequent
- Count occurrences
- Majority element
- Anagram
- Character count

Examples

- Valid Anagram
- Majority Element
- Top K Frequent

---

# 4. Prefix Sum

Purpose

Quickly calculate the sum of any subarray.

Example

Array

2 4 6 8

Prefix

0 2 6 12 20

Formula

Sum(L,R)

=

prefix[R+1]

-

prefix[L]

Time

Building Prefix → O(n)

Query → O(1)

---

Think Prefix Sum when

Question contains

- Sum of subarray
- Range sum
- Continuous subarray
- Running sum

Examples

- Range Sum Query
- Subarray Sum Equals K

---

# 5. Prefix + Suffix Pattern

Used when every element depends on everything except itself.

Example

Product Except Self

Input

1 2 3 4

Left Product

1 1 2 6

Right Product

24 12 4 1

Answer

24 12 8 6

---

Think Prefix + Suffix when

Question asks

"Everything except current element"

Examples

- Product of Array Except Self
- Rain Water (prefix/suffix max variant)

---

# Pattern Recognition Sheet

| Problem Says | Pattern |
|--------------|---------|
| Find two numbers | HashMap |
| Seen before | HashSet |
| Duplicate | HashSet |
| Count frequency | Frequency Map |
| Most frequent | Frequency Map + Heap |
| Range Sum | Prefix Sum |
| Continuous Subarray | Prefix Sum |
| Product Except Self | Prefix + Suffix |
| Consecutive Sequence | HashSet |

---

# Time Complexities

Array Access

O(1)

HashMap Lookup

O(1)

HashSet Lookup

O(1)

Frequency Count

O(n)

Prefix Sum Build

O(n)

Prefix Sum Query

O(1)

---

# Interview Questions

Easy

- Two Sum
- Contains Duplicate
- Valid Anagram
- Majority Element

Medium

- Product of Array Except Self
- Top K Frequent Elements
- Longest Consecutive Sequence
- Subarray Sum Equals K

Hard

- First Missing Positive

---

# Daily Checklist

□ Can I identify when to use HashMap?

□ Can I identify when to use HashSet?

□ Do I know Frequency Count?

□ Do I know Prefix Sum?

□ Do I know Prefix + Suffix?

□ Can I explain why each gives O(1) lookup?

If YES, you're ready for Arrays & Hashing interviews.