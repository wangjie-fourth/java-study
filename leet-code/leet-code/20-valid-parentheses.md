# 题目
给定一个只包括` '('，')'，'{'，'}'，'['，']' `的字符串`s`，判断字符串是否有效。 
有效字符串需满足： 
左括号必须用相同类型的右括号闭合。 
左括号必须以正确的顺序闭合。 

示例 1： 
输入：`s = "()"`
输出：`true`

示例 2： 
输入：`s = "()[]{}"`
输出：`true`

示例 3： 
输入：`s = "(]"`
输出：`false`

示例 4： 
输入：`s = "([)]"`
输出：`false`

示例 5： 
输入：`s = "{[]}"`
输出：`true`

提示： 
`1 <= s.length <= 104`
`s`仅由括号`'()[]{}'`组成 

# 解答
```java 
import java.util.Stack;

//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        char[] chars = s.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            Character item = chars[i];
            if (item == '(' || item == '[' || item == '{') {
                stack.push(item);
            } else if (item == ')') {
                if (stack.isEmpty() || stack.pop() != '(') {
                    return false;
                }
            } else if (item == ']') {
                if (stack.isEmpty() || stack.pop() != '[') {
                    return false;
                }
            } else if (item == '}') {
                if (stack.isEmpty() || stack.pop() != '{') {
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }
}
```

如果字符串可以包含其他字符串的话，怎么做？

---
https://leetcode-cn.com/problems/valid-parentheses/