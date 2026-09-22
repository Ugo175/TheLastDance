Problem: Contains Duplicate

Difficulty: Easy

### U - Understand
We need to determine if an array contains any duplicate values:
- Input: an array of integers
- Output: True if any value appears at least twice, False otherwise
- Edge cases: empty array, single element, all same elements, all unique elements

### M - Match
This is a hash set problem because:
- We need to check if we've seen a number before
- Set provides O(1) lookup and insertion
- Pattern: Tracking seen elements for duplicate detection

### P - Plan
1. Handle edge case: if array is empty, return False
2. Create an empty set to track seen numbers
3. Iterate through the array:
   - If current number is already in the set, return True (duplicate found)
   - Otherwise, add the number to the set
4. If we complete the loop without finding duplicates, return False

### I - Implement
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
```

### R - Run
Example walkthrough with nums = [1, 2, 3, 1]:
- seen = {}
- i=0: num=1, 1 not in seen, add to set: seen = {1}
- i=1: num=2, 2 not in seen, add to set: seen = {1, 2}
- i=2: num=3, 3 not in seen, add to set: seen = {1, 2, 3}
- i=3: num=1, 1 in seen, return True

### E - Evaluate
Time Complexity: O(n) where n is the length of the array
- Each lookup and insertion in the set is O(1) on average
- We perform n operations total

Space Complexity: O(n) in the worst case
- In the worst case (all unique elements), the set stores n elements
- Best case: O(1) if duplicate found early

Key Insight
Using a hash set allows us to detect duplicates in a single pass through the array, avoiding the O(n²) time complexity of a nested loop approach.

What I Learned
Hash sets are ideal for membership testing and duplicate detection problems. The trade-off is increased space usage for improved time complexity.
