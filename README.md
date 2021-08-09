# Leetcode notes

language: Python3

##Day1 (2021/Aug/09)

20. Valid Parentheses （Easy）


Algorithm：
1.Create a empty stack
2.Process every symbol from left to right
3.If we encounter a right branket i.e. "\(\[\{"
思路：括号匹配。生成空栈→从左到右从字符串里取括号→如是左括号，加入栈顶（stack.push(symbol)）→如是右括号，先判断栈空否→栈空则False；栈不空，移除栈顶的左括号 （top=stack.pop()）判断是否匹配，不匹配就False→当字符串取不到括号时，栈空则True，栈不空则False。




### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/YumengNUS/Yumeng.github.io/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
