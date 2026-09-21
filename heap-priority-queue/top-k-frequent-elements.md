Top K Frequent Elements

Difficulty: Medium

Plan

We need the `k` elements that appear most frequently.

The solution works in two steps:

1. Count the frequency of each number using a hash map.
2. Use a max heap to repeatedly extract the most frequent elements.

Since Python only provides a min heap, we store frequencies as negative values to simulate a max heap.

#Solution

class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int\]:
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

Time Complexity: O(n + m log m); where n is the length of nums and m is the number of unique elements

Space Complexity: O(m)

In the worst case, all elements are unique, so `m = n`, giving:

Time Complexity: O(n log n)
Space Complexity: O(n)
