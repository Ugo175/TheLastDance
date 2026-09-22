Problem: Top K Frequent Elements

Difficulty: Medium

### U - Understand
We need to find the k most frequent elements in an array:
- Input: array of integers and integer k
- Output: array of the k most frequent elements in any order
- Constraints: k is always valid (1 ≤ k ≤ number of unique elements)
- Edge cases: all elements same frequency, k equals number of unique elements

### M - Match
This is a heap/priority queue problem because:
- We need to find the "top k" elements based on frequency
- Heaps are optimized for extracting max/min elements
- Pattern: Count frequencies first, then use heap for selection

### P - Plan
1. Count the frequency of each number using a hash map
2. Use a max heap to repeatedly extract the most frequent elements:
   - Since Python only provides a min heap, store frequencies as negative values to simulate a max heap
   - Push (negative frequency, number) tuples into the heap
3. Extract the top k elements from the heap
4. Return the k most frequent elements

### I - Implement
```python
import heapq

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        freq = {}

        for num in nums:
            freq[num] = freq.get(num, 0) + 1

        heap = []

        for num, count in freq.items():
            heapq.heappush(heap, (-count, num))

        res = []

        for _ in range(k):
            count, num = heapq.heappop(heap)
            res.append(num)

        return res
```

### R - Run
Example walkthrough with nums = [1, 1, 1, 2, 2, 3], k = 2:
- freq = {1: 3, 2: 2, 3: 1}
- heap construction: push (-3, 1), (-2, 2), (-1, 3)
- heap = [(-3, 1), (-2, 2), (-1, 3)] (min heap by first element)
- Extract 1: pop (-3, 1), res = [1]
- Extract 2: pop (-2, 2), res = [1, 2]
- Return [1, 2]

### E - Evaluate
Time Complexity: O(n + m log m)
- n = length of nums array
- m = number of unique elements
- Building frequency map: O(n)
- Building heap: O(m log m)
- Extracting k elements: O(k log m)
- Total: O(n + m log m)

Space Complexity: O(m)
- Frequency map stores m elements
- Heap stores m elements
- Result array stores k elements

In the worst case, all elements are unique, so m = n:
- Time Complexity: O(n log n)
- Space Complexity: O(n)

Key Insight
Using a heap allows us to efficiently find the top k elements without fully sorting all elements. The key insight is using negative frequencies to simulate a max heap with Python's min heap implementation.

What I Learned
Heaps are ideal for "top k" problems where we need to extract the largest/smallest elements. The heap property gives us O(log n) extraction, which is more efficient than full sorting when k is much smaller than n.
