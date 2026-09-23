Problem: Maximum Average Subarray I

Difficulty: Easy

### U - Understand
We need to find the maximum average of any contiguous subarray of length k:
- Input: array of integers and integer k (subarray length)
- Output: maximum average value as a float
- The subarray must be contiguous (consecutive elements)
- Edge cases: k equals array length, k equals 1, all same values, negative numbers

### M - Match
This is a sliding window problem because:
- We need to examine contiguous subarrays of fixed length k
- We can slide a window of size k across the array
- When the window moves, we can efficiently update the sum by removing the leftmost element and adding the new rightmost element
- Pattern: Fixed-size sliding window for optimization

### P - Plan
1. Calculate the sum of the first k elements (initial window)
2. Set this as the initial max_sum
3. Slide the window from position k to the end of the array:
   - Remove the leftmost element from window_sum
   - Add the new rightmost element to window_sum
   - Update max_sum if current window_sum is larger
4. Return max_sum divided by k to get the average

### I - Implement
```python
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        array_length = len(nums) - 1
        left, right = 0, k - 1
        window_sum = sum(nums[:k])
        max_sum = window_sum

        while right < array_length:
            window_sum -= nums[left]
            right += 1
            window_sum += nums[right]
            left += 1

            max_sum = max(window_sum, max_sum)

        return max_sum / k
```

### R - Run
Example walkthrough with nums = [1, 12, -5, -6, 50, 3], k = 4:
- Initial window: [1, 12, -5, -6], sum = 2, max_sum = 2
- Slide: remove 1, add 50 → [12, -5, -6, 50], sum = 51, max_sum = 51
- Slide: remove 12, add 3 → [-5, -6, 50, 3], sum = 42, max_sum = 51
- Return 51 / 4 = 12.75

### E - Evaluate
Time Complexity: O(n) where n is the length of the array
- Initial sum calculation: O(k)
- Sliding window: O(n - k) iterations
- Total: O(n)

Space Complexity: O(1)
- Only using a few variables (left, right, window_sum, max_sum)
- No extra data structures needed

Key Insight
The key insight is that when sliding a fixed-size window, we don't need to recalculate the entire sum each time. We can efficiently update the sum by removing the element leaving the window and adding the element entering the window. This reduces the complexity from O(n*k) to O(n).

What I Learned
Sliding window is powerful for contiguous subarray problems. The pattern of "remove left, add right" allows efficient window updates without recomputing everything. This technique works well for fixed-size windows and can be adapted for variable-size windows too.