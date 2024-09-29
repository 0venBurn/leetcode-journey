# Leetcode 26. Remove Duplicates from sorted array

## Problem

Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in nums.

Consider the number of unique elements of nums to be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the unique elements in the order they were present in nums initially. The remaining elements of nums are not important as well as the size of nums.
Return k.

## Solution

```python
def remove_dupes(arr):
    l = 1
    for r in range(1, len(arr)):
        if arr[r] != arr[r - 1]:
            arr[l] = arr[r]
            l += 1


    return l
```

## Insight

- So this problem throws us a sorted array with potential duplicates. We gotta sort it in place, meaning no cheating with a new array!
- We need to figure out how to kick out the duplicates without messing up the order of the unique elements. Plus, we need to return the count of these unique elements.
- At first glance, you might think, "Hey, let's use a hashset to track the unique elements!" But hold up, that's extra space, and we're trying to do this in-place.
- Then you might consider swapping duplicates to the end of the array. But that's a lot of unnecessary movement, isn't it?
- Here's where it gets interesting: since the array is already sorted, duplicates will always be right next to each other. That's a big clue.
- So, what if we use two pointers? Let's call them 'left' and 'right':
  - The 'left' pointer can keep track of where we should put the next unique element we find.
  - The 'right' pointer can scan through the array, looking for these unique elements.
- We can start both pointers at the second element (index 1) because, hey, the first element is always unique where it is, right?
- As we move the 'right' pointer along, we can compare each element with the previous one:
  - If it's different, yipee. We've found a new unique element. We can place it where the 'left' pointer is and then move 'left' up one spot.
  - If it's the same, no issue. We just move on with the 'right' pointer.
- This way, we're not really "removing" duplicates. We're more like overwriting them with the next unique elements we find.
- In the end, the 'left' pointer will tell us how many unique elements we have. That's our return value
