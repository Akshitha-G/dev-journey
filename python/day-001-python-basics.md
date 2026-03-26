# Day 001 — Python basics + first LeetCode

**Date:** March 27, 2026
**Resources:** CodeWithHarry — 100 Days of Code (Videos 1–6)

---

## What I covered today

Watched the first 6 videos of CodeWithHarry's 100 Days of Code series. It was mostly setup and orientation — what Python is, where it's used, how to write your first lines, and how variables and data types work.

Topics across the videos:
- What Python is and why people use it
- Real-world applications — web dev, automation, data science, ML, scripting
- Modules and pip (installing external packages)
- Writing your first program with `print()`
- Comments — single line (`#`) and multi-line (`'''`)
- Variables, naming rules, and the core data types

---

## Notes

**print() and comments**
```python
print("Hello, world!")   # this is a comment

'''
this is a
multi-line comment
'''
```

**Variables — no need to declare a type, Python figures it out**
```python
name = "Akshitha"    # str
age = 21             # int
gpa = 9.2            # float
is_student = True    # bool
```

**The 4 basic data types**

| Type | Example | Notes |
|------|---------|-------|
| `int` | `10`, `-3` | whole numbers |
| `float` | `3.14`, `-0.5` | decimal numbers |
| `str` | `"hello"` | text, wrapped in quotes |
| `bool` | `True`, `False` | must be capitalised in Python |

You can always check what type a variable is:
```python
print(type(name))   # <class 'str'>
print(type(age))    # <class 'int'>
```

**pip and modules**
- Python has a standard library built in (like `math`, `os`)
- For everything else, you install with pip: `pip install package-name`
- Import before using: `import math` then `math.sqrt(16)`

---

## What confused me

The difference between `int` and `float` seemed obvious at first, but I wasn't sure what happens when you do math with them — like does `3 / 2` give `1` or `1.5`? Turns out in Python 3 it gives `1.5` (float). If you want integer division you use `//` which gives `1`. Good to know early.

---

## LeetCode — Two Sum (#1)

**Problem:** Given an array of integers and a target, return the indices of the two numbers that add up to the target.

The naive way is two nested loops — check every pair. That works but it's O(n²). The better way is to use a dictionary and do it in one pass.

**My approach:** As I walk through the array, for each number I calculate what value I'd *need* to pair with it to reach the target — that's the complement (`target - nums[i]`). I check if that complement has already been seen. If yes, I've found the pair. If not, I store the current number and its index in the dictionary and keep going.

```python
class Solution(object):
    def twoSum(self, nums, target):
        # Dictionary to store number and its index
        num_map = {}

        for i in range(len(nums)):
            # What do I need to pair with nums[i] to reach target?
            complement = target - nums[i]

            # If that number was already seen, we're done
            if complement in num_map:
                return [num_map[complement], i]

            # Otherwise, remember this number and where it was
            num_map[nums[i]] = i

        return []
```

**Why this works:**

Instead of looking forward ("is there something ahead that pairs with me?"), the dictionary lets you look backward ("was there something before that pairs with me?"). By the time you reach any number, all previous numbers are already stored — so a single `in` check is all you need.

**Example walkthrough — nums = [2, 7, 11, 15], target = 9:**
- i=0, num=2 → complement=7, not in map → store {2: 0}
- i=1, num=7 → complement=2, found in map at index 0 → return [0, 1] ✓

**What I used from today's learning:**
Dictionaries (`num_map = {}`), a `for` loop with `range()`, indexing into a list with `nums[i]`, and the `in` keyword to check if a key exists in a dict. Day 1 directly applied.

