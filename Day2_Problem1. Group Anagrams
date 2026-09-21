Group Anagrams

Difficulty: Medium

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]\]:
        if not strs:
            return []

        seen = {}

        for word in strs:
            ordered_word = "".join(sorted(word))

            if ordered_word not in seen:
                seen[ordered_word] = []

            seen[ordered_word].append(word)

        return list(seen.values())

Time Complexity: O(n · k log k), the loop runs n times, sorting each word takes O(klogk), where k is number of strings, and k is average length of a string. 
Therefore, the total time complexity is O(nlogk)

Space Complexity: O(n · k), the dictionary stores all words and their keys.

Where:
n = number of strings
k = average length of a string



