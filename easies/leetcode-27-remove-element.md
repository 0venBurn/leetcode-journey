# Leetcode 26. Remove Duplicates from sorted array

## Problem

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
Return k.

## Solution

```python
def remove_val(arr, val):
    l = 0
    for r in range(len(arr)):
        if arr[r] != val:
            arr[l] = arr[r]
            l += 1
    return l

```

## Insight

- This problem states that we must remove all occurrences of val in place. The number of vals not equal to val are k and the array just needs to be so that the first k numbers != val and after that it doesn't matter nor does the size of the arr.
- Considering this and the fact there are no stipulations of having to order the array in a certain manner it can become clear that we just need to loop through the array, detect the values != val and put them at the start. That's really it. To achieve this we can have two pointers, l and r. l will the first pointer and r will the loop pointer. We start l and r at 0 and then move through the array with r. If we find something != val then we just place that at l. Increment l and continue on as this will remove all occurrences of the val in the first k elements that are not val.

## Walk-through example

Let's walk through the algorithm using the array: `my_arr = [3, 2, 2, 3]` and `val = 3`

We'll use two pointers: `l` (left) starting at index 0, and `r` (right) also starting at index 0.

1. Initial state: `l = 0, r = 0`

   ```
   [3, 2, 2, 3]
    l
    r
   ```

2. `r` is at index 0 (value 3). It's equal to val.
   We do nothing and just move `r`.

   ```
   [3, 2, 2, 3]
    l
       r
   ```

3. `r` moves to index 1 (value 2). It's not equal to val.
   We set `arr[l] = arr[r]`, then increment `l`.

   ```
   [2, 2, 2, 3]
       l
          r
   ```

4. `r` is at index 2 (value 2). It's not equal to val.
   We set `arr[l] = arr[r]`, then increment `l`.

   ```
   [2, 2, 2, 3]
          l
             r
   ```

5. `r` is at index 3 (value 3). It's equal to val.
   We do nothing and just move `r`.

   ```
   [2, 2, 2, 3]
          l
                r
   ```

6. `r` has reached the end of the array. We're done.

Final state of the array: `[2, 2, 2, 3]`

The algorithm returns `l`, which is 2. This correctly indicates that there are 2 elements in the array that are not equal to val.
