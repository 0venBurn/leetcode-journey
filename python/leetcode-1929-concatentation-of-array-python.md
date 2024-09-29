# Leetcode 1929. Concatenation of Array

Given an integer array nums of length n, you want to create an array ans of length 2n where ans[i] == nums[i] and ans[i + n] == nums[i] for 0 <= i < n (0-indexed).

Specifically, ans is the concatenation of two nums arrays.

Return the array ans.

## Solution

```python
def get_concatentation(nums):
    res = []

    for concat in range(2):
        for num in nums:
            res.append(num)

    return res

```

## Insight

- This problem is fairly easy once you know what a concatenation is in which in basic terms is the joining of two things
- This problem wants us to concatenate the given array to itself.
- Possible solution for this is to just use the "+" operator in python however for the sake of
  modificatoin a nested loop with the range defined for the number of concatenations to take place is probably preferable given that if this question asked for three concatenations you could just change

```python
for concat in range(2)
```

to anything you want.
