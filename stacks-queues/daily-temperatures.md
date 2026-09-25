Problem: Daily Temperatures

Difficulty: Medium

### U - Understand
We need to find how many days you have to wait until a warmer temperature for each day:
- Input: array of integers representing daily temperatures
- Output: array where each element is the number of days to wait for a warmer temperature
- If no warmer day in the future, output 0 for that day
- Edge cases: strictly decreasing temperatures, strictly increasing temperatures, all same temperatures

### M - Match
This is a monotonic stack problem because:
- We need to find the next greater element for each position
- We can use a stack to keep track of indices of temperatures we haven't found a warmer day for
- The stack maintains temperatures in decreasing order (monotonic decreasing)
- When we find a warmer temperature, we resolve all previous colder days
- Pattern: Monotonic stack for next greater element problems

### P - Plan
1. Initialize answer array with all zeros
2. Create a stack to store indices of elements we haven't found their warmer days yet
3. Iterate through temperatures with index:
   - While stack is not empty and current temperature > temperature at stack's top index:
     - Pop the index from stack
     - Calculate days waited: current index - popped index
     - Update answer at popped index with this difference
   - Push current index onto stack
4. Return the answer array (indices remaining in stack will have 0, which is already set)

### I - Implement
```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        answer = [0] * len(temperatures)
        stack = []  # stores indices

        for i, temp in enumerate(temperatures):
            while stack and temp > temperatures[stack[-1]]:
                prev_day = stack.pop()
                answer[prev_day] = i - prev_day

            stack.append(i)

        return answer
```

### R - Run
Example walkthrough with temperatures = [73, 74, 75, 71, 69, 72, 76, 73]:
- i=0, temp=73: stack=[0]
- i=1, temp=74: 74>73, pop 0, answer[0]=1, stack=[1]
- i=2, temp=75: 75>74, pop 1, answer[1]=1, stack=[2]
- i=3, temp=71: stack=[2,3]
- i=4, temp=69: stack=[2,3,4]
- i=5, temp=72: 72>69, pop 4, answer[4]=1; 72>71, pop 3, answer[3]=2; stack=[2,5]
- i=6, temp=76: 76>72, pop 5, answer[5]=1; 76>75, pop 2, answer[2]=4; stack=[6]
- i=7, temp=73: stack=[6,7]
- Return [1,1,4,2,1,1,0,0]

### E - Evaluate
Time Complexity: O(n) where n is the length of temperatures array
- Each element is pushed onto the stack exactly once
- Each element is popped from the stack at most once
- Total operations: 2n = O(n)

Space Complexity: O(n)
- The answer array stores n elements
- The stack can store up to n elements in the worst case (decreasing temperatures)
- Total: O(n)

Key Insight
The key insight is using a monotonic decreasing stack. When we encounter a temperature that's warmer than the temperature at the top of the stack, we know we've found the answer for that previous day. By processing in this way, we resolve all previous days that this current temperature can serve as the "warmer day" for.

What I Learned
Monotonic stacks are powerful for "next greater/smaller element" problems. The stack maintains elements in a specific order (increasing or decreasing) and efficiently resolves previous elements when the order is violated. This pattern converts what could be an O(n²) nested loop problem into an O(n) solution.