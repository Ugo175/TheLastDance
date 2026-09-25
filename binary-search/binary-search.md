Problem: Binary Search

Difficulty: Easy

### U - Understand
We need to search for a target value in a sorted array using binary search:
- Input: sorted array of integers in ascending order and a target integer
- Output: index of target if found, -1 if not found
- The array is already sorted, which is key to the binary search algorithm
- Edge cases: empty array, target at beginning/end, target not present, array with one element

### M - Match
This is a binary search problem because:
- The array is sorted, which allows us to use divide and conquer
- We can eliminate half of the remaining elements with each comparison
- Binary search is the optimal algorithm for searching in sorted arrays
- Pattern: Two-pointer technique with left and right pointers converging

### P - Plan
1. Initialize left pointer at 0 and right pointer at n-1
2. While left <= right:
   - Calculate middle index: mid = (left + right) // 2
   - If nums[mid] equals target, return mid
   - If nums[mid] > target, target must be in left half: right = mid - 1
   - If nums[mid] < target, target must be in right half: left = mid + 1
3. If loop completes without finding target, return -1

### I - Implement
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return mid
            elif nums[mid] > target:
                right = mid - 1
            elif nums[mid] < target:
                left = mid + 1

        return -1
```

### R - Run
Example walkthrough with nums = [-1, 0, 3, 5, 9, 12], target = 9:
- left=0, right=5, mid=2, nums[2]=3 < 9, left=3
- left=3, right=5, mid=4, nums[4]=9 == 9, return 4

Example with target = 2:
- left=0, right=5, mid=2, nums[2]=3 > 2, right=1
- left=0, right=1, mid=0, nums[0]=-1 < 2, left=1
- left=1, right=1, mid=1, nums[1]=0 < 2, left=2
- left=2 > right=1, exit loop, return -1

### E - Evaluate
Time Complexity: O(log n) where n is the length of the array
- Each iteration eliminates half of the remaining elements
- Number of iterations: log₂(n)
- Much better than linear search O(n)

Space Complexity: O(1)
- Only using a few variables (left, right, mid)
- No extra data structures needed

Key Insight
The key insight is that in a sorted array, comparing the middle element to the target tells us which half to search next. If the middle element is greater than the target, the target (if it exists) must be in the left half. If it's smaller, the target must be in the right half. This halving continues until we find the target or exhaust the search space.

What I Learned
Binary search is a fundamental algorithm that leverages sorted data to achieve logarithmic time complexity. The pattern of maintaining left and right pointers and adjusting them based on comparison with the middle element is versatile and applies to many variations of search problems. Careful attention to the loop condition (left <= right) and pointer updates (mid ± 1) is crucial to avoid infinite loops or missed elements.