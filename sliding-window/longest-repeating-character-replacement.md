Problem: Longest Repeating Character Replacement

Difficulty: Medium

### U - Understand
We need to find the length of the longest substring that can be formed by replacing at most k characters:
- Input: a string s and integer k (maximum replacements allowed)
- Output: length of the longest substring after at most k character replacements
- We can replace any character with any other uppercase English letter
- The goal is to make all characters in the substring the same
- Edge cases: k equals string length, k equals 0, all same characters, all different characters

### M - Match
This is a sliding window problem with a frequency counter because:
- We need to find the longest valid substring
- A window is valid if (window length - max frequency) <= k
- We can track character frequencies using a Counter
- When the window becomes invalid, we shrink from the left
- Pattern: Variable-size sliding window with frequency tracking

### P - Plan
1. Initialize left pointer, Counter for character frequencies, and tracking variables
2. Expand the window by moving the right pointer:
   - Add current character to frequency counter
   - Update max frequency of any character in current window
   - Check if window is valid: (window length - max frequency) <= k
   - If invalid, shrink window from left until valid
   - Update longest length if current window is longer
3. Return the longest length found

### I - Implement
```python
from collections import Counter

class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        left = 0
        seen = Counter()
        length_s = len(s)
        longest, max_freq = 0, 0

        for right in range(length_s):
            seen[s[right]] += 1
            max_freq = max(max_freq, seen[s[right]])

            while (right - left + 1) - max_freq > k:
                seen[s[left]] -= 1
                left += 1

            longest = max(longest, right - left + 1)

        return longest
```

### R - Run
Example walkthrough with s = "ABAB", k = 2:
- right=0: 'A', seen={'A':1}, max_freq=1, window=1, valid (1-1<=2), longest=1
- right=1: 'B', seen={'A':1,'B':1}, max_freq=1, window=2, valid (2-1<=2), longest=2
- right=2: 'A', seen={'A':2,'B':1}, max_freq=2, window=3, valid (3-2<=2), longest=3
- right=3: 'B', seen={'A':2,'B':2}, max_freq=2, window=4, valid (4-2<=2), longest=4
- Return 4

Example with s = "AABABBA", k = 1:
- Build window and shrink when needed...
- The longest valid window is 4 (e.g., "AABA" or "ABBA")

### E - Evaluate
Time Complexity: O(n) where n is the length of the string
- Each character is added to the counter at most once
- Each character is removed from the counter at most once
- The while loop may seem nested, but total operations are bounded by 2n

Space Complexity: O(1) or O(26)
- The counter stores at most 26 entries (uppercase English letters)
- This is constant space regardless of input size

Key Insight
The key insight is that a window is valid if (window length - max frequency) <= k. This means we can replace all characters except the most frequent one to make the entire window uniform. We don't need to actually perform the replacements - we just need to ensure they're possible within the k limit.

What I Learned
Sliding window problems can involve complex validity conditions. The key is to identify what makes a window "valid" and efficiently check that condition. Tracking the maximum frequency allows us to determine validity without needing to know which character is most frequent. The window only grows or shrinks based on the validity condition, not on specific character choices.