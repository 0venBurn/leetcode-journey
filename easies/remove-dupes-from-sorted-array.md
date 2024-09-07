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

## Walk-through example

Let's walk through the algorithm using the array: `my_arr = [1, 3, 3, 4, 5, 5, 6]`

We'll use two pointers: `l` (left) starting at index 1, and `r` (right) also starting at index 1.

1. Initial state: `l = 1, r = 1`

   ```
   [1, 3, 3, 4, 5, 5, 6]
       l
       r
   ```

2. `r` is at index 1 (value 3). It's different from the previous element (1).
   We set `arr[l] = arr[r]` (which doesn't change anything in this case), then increment `l`.

   ```
   [1, 3, 3, 4, 5, 5, 6]
          l
          r
   ```

3. `r` moves to index 2 (value 3). It's the same as the previous element.
   We do nothing and just move `r`.

   ```
   [1, 3, 3, 4, 5, 5, 6]
          l
             r
   ```

4. `r` is at index 3 (value 4). It's different from the previous element (3).
   We set `arr[l] = arr[r]`, then increment `l`.

   ```
   [1, 3, 4, 4, 5, 5, 6]
             l
                r
   ```

5. `r` is at index 4 (value 5). It's different from the previous element (4).
   We set `arr[l] = arr[r]`, then increment `l`.

   ```
   [1, 3, 4, 5, 5, 5, 6]
                l
                   r
   ```

6. `r` is at index 5 (value 5). It's the same as the previous element.
   We do nothing and just move `r`.

   ```
   [1, 3, 4, 5, 5, 5, 6]
                l
                      r
   ```

7. `r` is at index 6 (value 6). It's different from the previous element (5).
   We set `arr[l] = arr[r]`, then increment `l`.

   ```
   [1, 3, 4, 5, 6, 5, 6]
                   l
                      r
   ```

8. `r` has reached the end of the array. We're done.

Final state of the array: `[1, 3, 4, 5, 6, 5, 6]`

The algorithm returns `l`, which is 5. This correctly indicates that there are 5 unique elements in the array.

Because the elements after index 4 (the 5th element) are not important and can be in any order. The important part is that the first 5 elements are the unique elements in their original order.
