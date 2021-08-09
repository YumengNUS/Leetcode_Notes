# Leetcode notes

language: Python3

### Q20. Valid Parentheses （Easy）

Algorithm：Stack

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

