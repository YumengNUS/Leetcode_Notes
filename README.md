# Leetcode notes

language: Python3

## 1.Stack

---
### Q32. Longest Valid Parentheses  (Hard)
---
Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

<strong>Algorithm</strong>:
Find the "()", and check if this "()" is concatenated with other "()". I use dictionary to record every "()"'s position and current length. 

1. When find a valid "()", calculate the length of them. Then Check if this "()" concatenate with other valid "()", if yes, get the length of that "()" using dictionary and add it to current length.

2. Store the position and total length of current "()" in th dictionary.

3. if current length is longer than longest length, longest = current


Notes: the length of parentheses = the position of ")" - the position of ")" + 1 
    
```python
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        longest_len = 0
        cur_len = 0
        stack = []
        len_dic={}
        position = []
        for i in range (0, len(s)):
            if s[i] == "(":
                stack.append(i)                     
            else:
                if stack != []:
                    if (stack[len(stack)-1] - 1) in position:
                        cur_len = len_dic[stack[len(stack)-1] - 1] + i - stack[len(stack)-1] + 1
                    else:
                        cur_len = i - stack[len(stack)-1] + 1
                    len_dic[i]=cur_len
                    position.append(i)
                    stack.pop()
                    if cur_len > longest_len:
                        longest_len = cur_len
                else:
                    cur_len = 0        
        return longest_len
        
```
    
<strong>Results:</strong>
Success
    
Runtime: 393 ms, faster than 5.45% of Python3 online submissions for Longest Valid Parentheses.
    
Memory Usage: 14.7 MB, less than 51.23% of Python3 online submissions for Longest Valid Parentheses.
    
---
### Q921. Minimum Add to Make Parentheses Valid (Medium)
---
You are given a parentheses string s. In one move, you can insert a parenthesis at any position of the string. Return the minimum number of moves required to make s valid.



```python
class Solution:
    def minAddToMakeValid(self, s: str) -> int:
        stack = 0
        min_add = 0
        for i in range (0,len(s)):
            if s[i] == "(":
                stack = stack+1
            elif s[i] == ")" and stack != 0:
                stack=stack-1
            else:
                min_add = min_add + 1
        min_add+=stack
        return min_add               
```

---
### Q387. First Unique Character in a String  (Easy)
---
Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.

<strong>Algorithm:</strong>
From the begining, checking repeating character after it one by one. If it's a repeating character, store it in a list (which is smaller than or equal to 26) so don't need to process this character again (saving runtime). Once non-repeating character is found, stop the loop.

????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????????

```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        index = -1
        repeat_list = []
        flag = 0
        for i in range (0, len(s)):            
            if s[i] not in repeat_list:
                flag = 0
                for j in range (i+1, len(s)):
                    if s[i] == s[j]:
                        flag = 1
                        repeat_list.append(s[j])
                        break
                if flag == 0:
                    index = i
                    break
        return index                 
```
<strong>Results:</strong>
Success 

Runtime: 144 ms, faster than 38.77% of Python3 online submissions for First Unique Character in a String.

Memory Usage: 14.5 MB, less than 21.54% of Python3 online submissions for First Unique Character in a String.

---
### Q20. Valid Parentheses ???Easy???
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

???????????????????????????????????????????????????????????????????????????????????????????????????????????????stack.push(symbol)??????????????????????????????????????????????????????False??????????????????????????????????????? ???top=stack.pop()????????????????????????????????????False?????????????????????????????????????????????True???????????????False???

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

Runtime: 32 ms, faster than 61.81% of Python3 online submissions for Valid Parentheses.

Memory Usage: 14.4 MB, less than 7.77% of Python3 online submissions for Valid Parentheses.

---
### Q225. Implement Stack using Queues ???Easy???
---
Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

<strong>Algorithm:</strong>
One queue is used as the main data structure, and the other one is utilized to implement the LIFO of stack. There are two methods according to the complexity. 1. If push is used more frequently than pop/top, use the rear of queue as "the stack top" (push: O(1), pop: O(n)); 2. Else if pop/top is used more frequently than push, use the front of queue as "the stack top"(push: O(n), pop: O(1)).

???????????????Queue????????????????????????????????????????????????stack???LIFO?????????queue?????????????????????????????????????????????1.???push???pop/top?????????????????????queue?????????????????????2.???pop/top?????????push???????????????queue????????????????????????????????????????????????2???

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

Runtime: 32 ms, faster than 52.32% of Python3 online submissions for Implement Stack using Queues.

Memory Usage: 14.5 MB, less than 11.54% of Python3 online submissions for Implement Stack using Queues.

<strong>Other solution:</strong>One queue: push: O(n), pop: O(1)
    
When we push an element into a queue, it will be stored at back of the queue due to queue's properties. But we need to implement a stack, where last inserted element should be in the front of the queue, not at the back. To achieve this we can <strong>invert the order of queue elements</strong> when pushing a new element.

![image](https://user-images.githubusercontent.com/49022041/128711466-e103f991-07f8-4f63-a605-66a9ac2b33c3.png)

---
### Q155. Min Stack???Easy???
---
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

<strong>Algorithm</strong>: Create a main stack to save data, and a aux list/stack to save the min elements in every position in that stack. Retrieving the minimum element during every push operation can save runtime and memory usage.

Notes: When building a stack with a specific task (Get Min), Overfitting to save runtime and memory usage is acceptable.

????????????????????????????????????????????????/?????????????????????????????????????????????????????????????????????????????????????????????????????????


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

Runtime: 60 ms, faster than 73.43% of Python3 online submissions for Min Stack.

Memory Usage: 17.9 MB, less than 98.68% of Python3 online submissions for Min Stack.






