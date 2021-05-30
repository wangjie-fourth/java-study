# 题目
设计一个支持`push`，`pop`，`top`操作，并能在常数时间内检索到最小元素的栈。 
`push(x)` —— 将元素 x 推入栈中。 
`pop()` —— 删除栈顶的元素。 
`top()` —— 获取栈顶元素。 
`getMin()` —— 检索栈中的最小元素。 

示例: 
输入：
`["MinStack","push","push","push","getMin","pop","top","getMin"]`
`[[],[-2],[0],[-3],[],[],[],[]]`
输出：
`[null,null,null,null,-3,null,0,-2]`
解释：
```java 
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```
提示： 
`pop`、`top`和`getMin`操作总是在非空栈上调用。 

# 解法
```java 
import java.util.Stack;

//leetcode submit region begin(Prohibit modification and deletion)
class MinStack {
    private Stack<Integer> minStackImpl;
    private Stack<Integer> stackImpl;

    /** initialize your data structure here. */
    public MinStack() {
        minStackImpl = new Stack<>();
        stackImpl = new Stack<>();
    }
    
    public void push(int x) {
        if (minStackImpl.isEmpty()) {
            minStackImpl.push(x);
        } else if (minStackImpl.peek() >= x) {
            minStackImpl.push(x);
        }
        stackImpl.push(x);
    }
    
    public void pop() {
        if (minStackImpl.isEmpty() || minStackImpl.peek().equals(stackImpl.pop())) {
            minStackImpl.pop();
        }
    }
    
    public int top() {
        return stackImpl.peek();
    }
    
    public int getMin() {
        return minStackImpl.peek();
    }
}
```
---
https://leetcode-cn.com/problems/min-stack/