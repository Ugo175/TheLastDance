Problem: Min Stack

Difficulty: Medium

### U - Understand
We need to implement a stack that supports push, pop, top, and retrieving the minimum element in constant time:
- Operations required:
  - push(val): push element onto stack
  - pop(): remove element from top of stack
  - top(): get top element
  - getMin(): retrieve minimum element in stack
- All operations must run in O(1) time complexity
- Edge cases: empty stack, duplicate minimum values, pushing after popping

### M - Match
This is a stack problem with an auxiliary data structure because:
- We need a regular stack for normal stack operations
- We need a way to track the minimum element efficiently
- Using a secondary stack (min_stack) allows O(1) minimum retrieval
- Pattern: Auxiliary stack for tracking metadata alongside main stack

### P - Plan
1. Initialize two stacks: main stack and min_stack
2. For min_stack, initialize with infinity to handle edge cases
3. For push operation:
   - Push value onto main stack
   - Push min(current min, new value) onto min_stack
4. For pop operation:
   - Pop from both stacks to maintain synchronization
5. For top operation:
   - Return top element from main stack
6. For getMin operation:
   - Return top element from min_stack (which is current minimum)

### I - Implement
```python
class MinStack:

    def __init__(self):
        self.stack = []
        self.min_stack = [float('inf')]

    def push(self, value: int) -> None:
        self.stack.append(value)
        self.min_stack.append(min(self.min_stack[-1], value))

    def pop(self) -> None:
        self.stack.pop()
        self.min_stack.pop()

    def top(self) -> int:
        return self.stack[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]
```

### R - Run
Example operations:
- push(-2): stack=[-2], min_stack=[inf, -2]
- push(0): stack=[-2, 0], min_stack=[inf, -2, -2]
- push(-3): stack=[-2, 0, -3], min_stack=[inf, -2, -2, -3]
- getMin(): returns -3 (top of min_stack)
- pop(): stack=[-2, 0], min_stack=[inf, -2, -2]
- top(): returns 0
- getMin(): returns -2

### E - Evaluate
Time Complexity: O(1) for all operations
- push: O(1) - append operations are constant time
- pop: O(1) - pop operations are constant time
- top: O(1) - accessing last element is constant time
- getMin: O(1) - accessing last element is constant time

Space Complexity: O(n) where n is the number of elements
- We maintain two stacks, each storing n elements
- The min_stack stores the minimum at each level to handle pops correctly

Key Insight
The key insight is that we need to track the minimum at each level of the stack, not just the global minimum. When we pop elements, we need to know what the minimum was before that element was pushed. By storing the running minimum in a parallel stack, we can efficiently retrieve the minimum for the current stack state.

What I Learned
When designing data structures, sometimes we need auxiliary structures to maintain additional information. The pattern of parallel stacks (or arrays) to track metadata alongside the main data is powerful. The key is ensuring that both structures stay synchronized during all operations.