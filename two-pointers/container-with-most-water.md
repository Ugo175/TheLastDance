Problem: Container With Most Water

Difficulty: Medium

### U - Understand
We need to find the maximum area of water that can be contained:
- Input: array of positive integers representing heights of vertical lines
- Output: maximum area of water that can be contained between two lines
- Area calculation: min(height[left], height[right]) × (right - left)
- Constraints: at least 2 lines, heights are positive integers
- Edge cases: all same heights, strictly increasing/decreasing heights

### M - Match
This is a two-pointer problem because:
- We need to find the optimal pair of lines
- Starting from the widest container and moving inward makes sense
- The area is limited by the shorter line, so we should move that pointer
- Pattern: Two pointers with greedy approach for optimization

### P - Plan
1. Handle edge case: if array is empty, return 0
2. Initialize max_area = 0, left pointer at 0, right pointer at n-1
3. While left < right:
   - Calculate current area using the shorter height × width
   - Update max_area if current area is larger
   - Move the pointer pointing to the shorter line inward:
     - If left height > right height, move right pointer left
     - Otherwise, move left pointer right
4. Return max_area

### I - Implement
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        if not height:
            return 0

        n = len(height)
        max_area = 0
        left, right = 0, n - 1

        while left < right:
            area = min(height[left], height[right]) * (right - left)

            max_area = max(area, max_area)

            if height[left] > height[right]:
                right -= 1
            else:
                left += 1

        return max_area
```

### R - Run
Example walkthrough with height = [1, 8, 6, 2, 5, 4, 8, 3, 7]:
- left = 0, right = 8: area = min(1, 7) × 8 = 1 × 8 = 8, max_area = 8
- height[0] < height[8], move left: left = 1
- left = 1, right = 8: area = min(8, 7) × 7 = 7 × 7 = 49, max_area = 49
- height[1] > height[8], move right: right = 7
- left = 1, right = 7: area = min(8, 3) × 6 = 3 × 6 = 18, max_area = 49
- height[1] > height[7], move right: right = 6
- left = 1, right = 6: area = min(8, 8) × 5 = 8 × 5 = 40, max_area = 49
- height[1] == height[6], move left: left = 2
- Continue until left >= right...
- Final max_area = 49

### E - Evaluate
Time Complexity: O(n) where n is the length of the array
- Each iteration moves at least one pointer
- In the worst case, we make n-1 comparisons
- Much better than O(n²) brute force approach checking all pairs

Space Complexity: O(1)
- Only using a few variables (max_area, left, right, area)
- No extra data structures needed

Key Insight
The key insight is that the area is limited by the shorter line. When we move the pointer pointing to the taller line, we're guaranteed to get a smaller area (width decreases, height is still limited by the shorter line). By always moving the shorter line's pointer, we might find a taller line that could give us a larger area.

What I Learned
Greedy two-pointer approach works well for optimization problems with sorted or spatial constraints. The strategy of eliminating impossible solutions (moving the shorter line) helps efficiently find the optimal solution without checking all possibilities.