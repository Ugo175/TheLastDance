2026-09-19

Problem: Two Sum

Difficulty: Easy

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

Time Complexity: O(n)

Space Complexity: O(n)

Key Insight
Use a hash map to store previously seen values.

What I Learned
Hash maps often trade memory for speed by reducing nested loops.
  
