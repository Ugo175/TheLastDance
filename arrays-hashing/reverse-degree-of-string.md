Problem: Reverse Degree of a String

Difficulty: Easy

### U - Understand
We need to calculate the "reverse degree" of a string where:
- Each letter has a degree based on its reverse position in the alphabet (a=26, b=25, ..., z=1)
- The total degree is the sum of each letter's degree multiplied by its (1-indexed) position in the string
- Input: a string s containing only lowercase letters
- Output: an integer representing the total reverse degree

### M - Match
This is a hash map problem because:
- We need to map each letter to its reverse alphabet position
- We need efficient lookup for each character in the string
- Pattern: Character-to-value mapping using dictionary/hash map

### P - Plan
1. Create a string containing all lowercase letters in order
2. Build a hash map where each letter maps to its reverse position (a=26, b=25, ..., z=1)
3. Initialize a product variable to 0
4. Iterate through the input string:
   - For each character at position i, multiply its degree by (i+1) for 1-indexed position
   - Add this product to the running total
5. Return the final product

### I - Implement
```python
from collections import defaultdict

class Solution:
    def reverseDegree(self, s: str) -> int:
        alphabet = "abcdefghijklmnopqrstuvwxyz"
        storage = defaultdict()
        num = 26
        product = 0

        # Build hash map: a=26, b=25, ..., z=1
        for i in range(26):
            storage[alphabet[i]] = num
            num -= 1

        # Calculate total degree with position weighting
        for i in range(len(s)):
            product += storage[s[i]] * (i + 1)

        return product
```

### R - Run
Example walkthrough with s = "abc":
- storage = {'a': 26, 'b': 25, 'c': 24, ..., 'z': 1}
- i=0: product += storage['a'] * 1 = 26 * 1 = 26
- i=1: product += storage['b'] * 2 = 25 * 2 = 50, total = 76
- i=2: product += storage['c'] * 3 = 24 * 3 = 72, total = 148
- Return 148

### E - Evaluate
Time Complexity: O(n) where n is the length of the string
- Building the hash map: O(26) = O(1) since alphabet size is constant
- Iterating through the string: O(n)
- Total: O(n)

Space Complexity: O(1)
- Hash map stores 26 entries (constant size)
- Product variable: O(1)
- Total: O(1)

Key Insight
Using a hash map allows O(1) lookup for each character's degree, making the overall solution efficient. The key insight is precomputing the reverse alphabet positions once, then using simple arithmetic for the final calculation.

What I Learned
Hash maps are excellent for character-to-value mappings, especially when the mapping needs to be looked up repeatedly. Precomputing values that don't change during the iteration is a common optimization pattern.
