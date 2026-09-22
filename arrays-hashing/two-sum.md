Problem: Two Sum

Difficulty: Easy

Date: 2026-09-19

### U - Understand
We need to find two numbers in an array that add up to a specific target:
- Input: array of integers and a target integer
- Output: indices of the two numbers that add up to target
- Constraints: exactly one valid solution exists, can't use same element twice
- Edge cases: negative numbers, large numbers, array with 2 elements

### M - Match
This is a hash map problem because:
- We need to find complement of current number (target - current)
- Hash map provides O(1) lookup for previously seen numbers
- Pattern: Complement searching with hash map

### P - Plan
1. Handle edge case: if array is empty, return empty array
2. Create a hash map to store number -> index mapping
3. Iterate through the array with index:
   - Calculate complement = target - current number
   - If complement exists in hash map, return [index of complement, current index]
   - Otherwise, store current number with its index in the hash map
4. Since exactly one solution is guaranteed, we'll always return within the loop

### I - Implement
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        if not nums:
            return []

        seen = {}
        for i, num in enumerate(nums):
            complement = target - num

            if complement in seen:
                return [seen[complement], i]

            seen[num] = i
```

### R - Run
Example walkthrough with nums = [2, 7, 11, 15], target = 9:
- seen = {}
- i=0: num=2, complement=7, 7 not in seen, store {2: 0}
- i=1: num=7, complement=2, 2 in seen at index 0, return [0, 1]

### E - Evaluate
Time Complexity: O(n) where n is the length of the array
- Each lookup and insertion in the hash map is O(1) on average
- We perform n operations total

Space Complexity: O(n) in the worst case
- In the worst case, we store n-1 elements before finding the solution
- Best case: O(1) if solution found early

Key Insight
Instead of checking all pairs (which would be O(n²)), we can check if the complement of the current number has been seen before. This transforms the problem from searching to a single lookup operation.

What I Learned
Hash maps often trade memory for speed by reducing nested loops. The key insight is to think about what information would be useful to have "already computed" when processing each element.
  
