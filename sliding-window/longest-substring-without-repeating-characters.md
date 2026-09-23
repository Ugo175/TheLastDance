Problem: Longest Substring Without Repeating Characters

Difficulty: Medium

### U - Understand
We need to find the length of the longest substring without repeating characters:
- Input: a string
- Output: integer representing the length of the longest substring with all unique characters
- Substring must be contiguous
- Edge cases: empty string, all same characters, all unique characters, string with spaces

### M - Match
This is a sliding window problem with a hash set because:
- We need to find the longest contiguous substring with unique characters
- We can use a sliding window with left and right pointers
- A hash set helps us track which characters are currently in the window
- When we encounter a duplicate, we shrink the window from the left
- Pattern: Variable-size sliding window with hash set for uniqueness tracking

### P - Plan
1. Initialize a set to track characters in current window
2. Initialize left pointer and longest length variables to 0
3. Expand the window by moving the right pointer:
   - If current character is already in the set, shrink window from left until it's not
   - Add current character to the set
   - Update longest length if current window is longer
4. Return the longest length found

### I - Implement
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        seen = set()
        left, longest = 0, 0
        length_s = len(s)

        for right in range(length_s):
            while s[right] in seen:
                seen.remove(s[left])
                left += 1

            seen.add(s[right])
            longest = max(longest, (right - left) + 1)

        return longest
```

### R - Run
Example walkthrough with s = "abcabcbb":
- right=0: 'a' not in seen, add 'a', seen={'a'}, longest=1
- right=1: 'b' not in seen, add 'b', seen={'a','b'}, longest=2
- right=2: 'c' not in seen, add 'c', seen={'a','b','c'}, longest=3
- right=3: 'a' in seen, remove 'a', left=1, seen={'b','c'}
- 'a' not in seen, add 'a', seen={'b','c','a'}, longest=3
- right=4: 'b' in seen, remove 'b', left=2, seen={'c','a'}
- 'b' not in seen, add 'b', seen={'c','a','b'}, longest=3
- Continue pattern...
- Final longest = 3

### E - Evaluate
Time Complexity: O(n) where n is the length of the string
- Each character is added to the set at most once
- Each character is removed from the set at most once
- The while loop may seem nested, but total operations are bounded by 2n

Space Complexity: O(min(n, m)) where m is the size of the character set
- In the worst case, the set stores all unique characters in the string
- For ASCII characters, this is bounded by 128 or 256
- For Unicode, this could be larger but still bounded by character set size

Key Insight
The key insight is using a sliding window that expands when we find new characters and contracts when we encounter duplicates. The hash set allows O(1) membership testing, making the overall solution efficient. We only move the left pointer when necessary to maintain the "no repeating characters" property.

What I Learned
Variable-size sliding windows are powerful for substring problems. The combination of sliding window with hash set for tracking uniqueness is a common pattern. The key is understanding when to expand (add new elements) and when to contract (remove duplicates) the window.