Problem: Group Anagrams

Difficulty: Medium

### U - Understand
We need to group strings that are anagrams of each other:
- Input: array of strings
- Output: array of arrays, where each inner array contains strings that are anagrams
- Anagrams: strings with same characters in different orders (e.g., "eat", "tea", "ate")
- Edge cases: empty array, single string, strings of different lengths, duplicate strings

### M - Match
This is a hash map problem because:
- Anagrams have the same sorted version (e.g., "eat" and "tea" both sort to "aet")
- We can use sorted string as a key to group anagrams
- Pattern: Using transformed version as key for grouping

### P - Plan
1. Handle edge case: if array is empty, return empty array
2. Create a hash map to store sorted_word -> list of anagrams
3. Iterate through each word in the input array:
   - Sort the characters of the word to create a key
   - If key doesn't exist in hash map, initialize empty list
   - Append the original word to the list for that key
4. Return all values from the hash map as the result

### I - Implement
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        if not strs:
            return []

        seen = {}

        for word in strs:
            ordered_word = "".join(sorted(word))

            if ordered_word not in seen:
                seen[ordered_word] = []

            seen[ordered_word].append(word)

        return list(seen.values())
```

### R - Run
Example walkthrough with strs = ["eat", "tea", "tan", "ate", "nat", "bat"]:
- seen = {}
- "eat": sorted = "aet", seen = {"aet": ["eat"]}
- "tea": sorted = "aet", seen = {"aet": ["eat", "tea"]}
- "tan": sorted = "ant", seen = {"aet": ["eat", "tea"], "ant": ["tan"]}
- "ate": sorted = "aet", seen = {"aet": ["eat", "tea", "ate"], "ant": ["tan"]}
- "nat": sorted = "ant", seen = {"aet": ["eat", "tea", "ate"], "ant": ["tan", "nat"]}
- "bat": sorted = "abt", seen = {"aet": ["eat", "tea", "ate"], "ant": ["tan", "nat"], "abt": ["bat"]}
- Return [["eat", "tea", "ate"], ["tan", "nat"], ["bat"]]

### E - Evaluate
Time Complexity: O(n · k log k)
- n = number of strings
- k = average length of a string
- Sorting each string takes O(k log k)
- We do this for n strings

Space Complexity: O(n · k)
- The dictionary stores all words and their sorted keys
- In the worst case, each word is its own anagram group

Where:
n = number of strings
k = average length of a string

Key Insight
The key insight is that all anagrams sort to the same string. By using the sorted version as a hash map key, we can automatically group anagrams together in a single pass.

What I Learned
String transformation (like sorting) can be used to create hash map keys for grouping problems. This pattern is useful whenever items that should be grouped together share a common transformed representation.



