Problem: Valid Parentheses

Difficulty: Easy

### U - Understand
We need to determine if a string of parentheses is valid:
- Input: a string containing only characters '(', ')', '{', '}', '[', ']'
- Output: True if the string is valid, False otherwise
- Valid means:
  - Open brackets must be closed by the same type of brackets
  - Open brackets must be closed in the correct order
  - Every close bracket has a corresponding open bracket of the same type
- Edge cases: empty string, odd length string, only opening brackets, only closing brackets

### M - Match
This is a stack problem because:
- We need to match opening and closing brackets in the correct order
- Stack follows LIFO (Last In, First Out) which matches the nesting nature of brackets
- When we encounter a closing bracket, we need to check the most recent opening bracket
- Pattern: Using stack for matching pairs and nested structures

### P - Plan
1. Handle edge case: if string length is odd, return False (can't have valid pairs)
2. Create a mapping of closing brackets to their corresponding opening brackets
3. Initialize an empty stack
4. Iterate through each character in the string:
   - If it's an opening bracket, push it onto the stack
   - If it's a closing bracket:
     - If stack is empty, return False (no matching opening bracket)
     - Pop from stack and check if it matches the expected opening bracket
     - If it doesn't match, return False
5. After processing all characters, return True if stack is empty, False otherwise

### I - Implement
```python
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s) % 2 != 0:
            return False

        pairs = {')': '(', ']': '[', '}': '{'}
        stack = []

        for ch in s:
            if ch in "([{":
                stack.append(ch)
            else:
                if not stack:
                    return False

                if stack.pop() != pairs[ch]:
                    return False

        return not stack
```

### R - Run
Example walkthrough with s = "()[]{}":
- '(' is opening, push: stack = ['(']
- ')' is closing, pop '(' matches ')', stack = []
- '[' is opening, push: stack = ['[']
- ']' is closing, pop '[' matches ']', stack = []
- '{' is opening, push: stack = ['{']
- '}' is closing, pop '{' matches '}', stack = []
- Stack is empty, return True

Example with s = "(]":
- '(' is opening, push: stack = ['(']
- ']' is closing, pop '(' doesn't match ']', return False

Example with s = "([)]":
- '(' push, '[' push, ')' closing expects '(' but gets '[', return False

### E - Evaluate
Time Complexity: O(n) where n is the length of the string
- We iterate through the string once
- Each push and pop operation is O(1)
- Total operations: O(n)

Space Complexity: O(n) in the worst case
- In the worst case (all opening brackets), the stack stores n/2 elements
- The pairs dictionary has constant size (3 entries)
- Total: O(n)

Key Insight
The key insight is that a stack naturally handles the nesting structure of brackets. The most recent opening bracket must be closed first (LIFO). By using a stack, we can efficiently check if closing brackets match the most recent opening bracket in the correct order.

What I Learned
Stacks are ideal for problems involving nested structures or matching pairs where order matters. The pattern of "push when opening, pop and check when closing" is a classic stack application. Early validation (like checking odd length) can provide quick rejections and improve efficiency.