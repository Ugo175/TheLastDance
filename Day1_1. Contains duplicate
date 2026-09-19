Problem: Contains Duplicate

Difficulty: Easy

Time Complexity: O(n)

Space Complexity: O(n)

Key Insight

Use a hash set to keep track of numbers we've already seen.

As we iterate through the array:
- If the current number is already in the set, we've found a duplicate and can immediately return `True`.
- Otherwise, add the number to the set and continue.

Solution:

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        if not nums:
            return False

        seen = set()

        for num in nums:
            if num in seen:
                return True
            seen.add(num)

        return False
