# Leetcode notes

language: Python3

## 1.Stack

---
### Q20. Valid Parentheses （Easy）
---
<strong>Algorithm:</strong> Stack

1.Create an empty stack; 

2.Create a dictionary of corresponding relation of different brankets; 

3.Process every symbol in the str from left to right; 

4(if).If we encounter a left branket i.e. "\(\[\{", push it into the top of our stack; 

4(else).Else if we encounter a right branket i.e. "\)\]\}", 

&emsp;&emsp;5(if).If the stack is Empty, flag = False;

&emsp;&emsp;5(else).Else if the stack is not Empty, remove the symbol in the stack top;

&emsp;&emsp;&emsp;&emsp;6.If this stack top doesn't matches the processing symbol,flag = False;

7.After Processing all symbols in the str, if stack is not empty or flag == Flase, return False; else return True.

思路：括号匹配。生成空栈→从左到右从字符串里取括号→如是左括号，加入栈顶（stack.push(symbol)）→如是右括号，先判断栈空否→栈空则False；栈不空，移除栈顶的左括号 （top=stack.pop()）判断是否匹配，不匹配就False→当字符串取不到括号时，栈空则True，栈不空则False。

<strong>My solution:</strong>
```python
class Stack:
    def __init__(self):
        self.data = []
    def push(self,symbol):
        self.data.append(symbol)
    def pop(self):
        top = self.data.pop()
        return top
    def isEmpty(self):
        return bool(self.data==[])
        

class Solution:
    def isValid(self, s: str) -> bool:
        stack = Stack()
        balanced = True
        dic = {"(":")", "[":"]", "{":"}"}
        for i in range(0, len(s)):
            symbol = s[i]
            if symbol in "({[":
                stack.push(symbol)
            else:
                if stack.isEmpty()==True:
                    balanced = False
                else:
                    top = stack.pop()
                    if dic[top] != symbol:
                        balanced = False
        if stack.isEmpty() and balanced:
               return True
        else:
               return False              
```

<strong>Results:</strong>
Success

Details:

Runtime: 32 ms, faster than 61.81% of Python3 online submissions for Valid Parentheses.

Memory Usage: 14.4 MB, less than 7.77% of Python3 online submissions for Valid Parentheses.

---
### Q225. Implement Stack using Queues （Easy）
---
Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

<strong>Algorithm:</strong>
One queue is used as the main data structure, and the other one is utilized to implement the LIFO of stack. There are two methods according to the complexity. 1. If push is used more frequently than pop/top, use the rear of queue as "the stack top" (push: O(1), pop: O(n)); 2. Else if pop/top is used more frequently than push, use the front of queue as "the stack top"(push: O(n), pop: O(1)).

思路：一个Queue做主要数据结构，另一个辅助其实现stack的LIFO。根据queue的头尾方向可以有两种实现方式：1.当push比pop/top操作频繁时，将queue后端当作栈顶；2.当pop/top操作比push频繁时，将queue前端用作栈顶。代码中展示的是方法2。

<strong>My solution:</strong>

```python
class MyStack:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.queue_main = []
        self.queue_aux = []

    def push(self, x: int) -> None:
        """
        Push element x onto stack.
        """
        for i in range (0, len(self.queue_main)):
            self.queue_aux.insert(0,self.queue_main.pop())
        self.queue_main.insert(0,x)
        for i in range (0, len(self.queue_aux)):
            self.queue_main.insert(0,self.queue_aux.pop())

    def pop(self) -> int:
        """
        Removes the element on top of the stack and returns that element.
        """
        return self.queue_main.pop()

    def top(self) -> int:
        """
        Get the top element.
        """
        return self.queue_main[len(self.queue_main)-1]

    def empty(self) -> bool:
        """
        Returns whether the stack is empty.
        """
        return self.queue_main == []

# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```
<strong>Results:</strong>
Success

Details 

Runtime: 32 ms, faster than 52.32% of Python3 online submissions for Implement Stack using Queues.

Memory Usage: 14.5 MB, less than 11.54% of Python3 online submissions for Implement Stack using Queues.

<strong>Other solution:</strong>One queue: push: O(n), pop: O(1)
    
When we push an element into a queue, it will be stored at back of the queue due to queue's properties. But we need to implement a stack, where last inserted element should be in the front of the queue, not at the back. To achieve this we can <strong>invert the order of queue elements</strong> when pushing a new element.

![image](https://user-images.githubusercontent.com/49022041/128711466-e103f991-07f8-4f63-a605-66a9ac2b33c3.png)

---
### Q155. Min Stack（Easy）
---
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

<strong>Algorithm</strong>: Create a main stack to save data, and a aux list/stack to save the min elements in every position in that stack. Retrieving the minimum element during every push operation can save runtime and memory usage.

Notes: When building a stack with a specific task (Get Min), Overfitting to save runtime and memory usage is acceptable.

思路：建立栈的同时建立另一个列表/栈去存储主栈中每一个位置对应的最小值。从而节省查找最小值的空间与时间。


```python
class MinStack:
    def __init__(self):
        """
        initialize your data structure here.
        """
        self.elems = []
        self.min_elem = []
        
    def push(self, val: int) -> None:
        self.elems.append(val)
        if len(self.min_elem) == 0:   
            self.min_elem.append(val)
        elif val < self.min_elem[len(self.min_elem)-1]:
            self.min_elem.append(val)
        else:
            self.min_elem.append(self.min_elem[len(self.min_elem)-1])

    def pop(self) -> None:
        self.elems.pop()
        self.min_elem.pop()

    def top(self) -> int:
        return self.elems[len(self.elems)-1]

    def getMin(self) -> int:
        return self.min_elem[len(self.min_elem)-1]

# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(val)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
<strong>Results:</strong>
Success

Details 

Runtime: 60 ms, faster than 73.43% of Python3 online submissions for Min Stack.

Memory Usage: 17.9 MB, less than 98.68% of Python3 online submissions for Min Stack.
