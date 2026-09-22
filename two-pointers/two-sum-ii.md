Problem: Two Sum II - Input Array Is Sorted

Difficulty: Medium

### U - Understand
We need to find two numbers in a sorted array that add up to a specific target:
- Input: sorted array of integers (ascending order) and a target integer
- Output: 1-indexed indices of the two numbers that add up to target
- Constraints: exactly one valid solution exists, can't use same element twice
- Edge cases: negative numbers, large numbers, array with 2 elements
- Key difference from Two Sum I: array is already sorted

### M - Match
This is a two-pointer problem because:
- The array is sorted, which allows us to use the two-pointer technique
- We can start from both ends and move inward based on the sum
- Pattern: Two pointers with sorted array for finding pairs

### P - Plan
1. Initialize left pointer at start (index 0) and right pointer at end (index n-1)
2. While left < right:
   - Calculate current_sum = numbers[left] + numbers[right]
   - If current_sum equals target, return [left+1, right+1] (1-indexed)
   - If current_sum < target, move left pointer right (need larger sum)
   - If current_sum > target, move right pointer left (need smaller sum)
3. Since exactly one solution is guaranteed, we'll always return within the loop

### I - Implement
```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        left = 0
        right = len(numbers) - 1

        while left < right:
            current_sum = numbers[left] + numbers[right]

            if current_sum == target:
                return [left + 1, right + 1]
            elif current_sum < target:
                left += 1
            else:
                right -= 1

        return []
```

### R - Run
Example walkthrough with numbers = [2, 7, 11, 15], target = 9:
- left = 0, right = 3
- current_sum = 2 + 15 = 17 > 9, move right: right = 2
- current_sum = 2 + 11 = 13 > 9, move right: right = 1
- current_sum = 2 + 7 = 9 == target, return [1, 2]

### E - Evaluate
Time Complexity: O(n) where n is the length of the array
- Each iteration moves at least one pointer
- In the worst case, we make n-1 comparisons
- Much better than O(n²) brute force approach

Space Complexity: O(1)
- Only using a few variables (left, right, current_sum)
- No extra data structures needed

Key Insight
Since the array is sorted, we can use the two-pointer technique to efficiently find the target sum. If the current sum is too small, we need a larger number (move left pointer right). If too large, we need a smaller number (move right pointer left).

What I Learned
The two-pointer technique is powerful for sorted arrays. It reduces the problem from O(n²) to O(n) by leveraging the sorted property to make intelligent decisions about which pointer to move.