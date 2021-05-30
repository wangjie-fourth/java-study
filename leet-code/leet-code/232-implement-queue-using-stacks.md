# 题目
请你仅使用两个栈实现先入先出队列。队列应当支持一般队列的支持的所有操作`（push、pop、peek、empty）`： 
实现`MyQueue`类： 
`void push(int x)` 将元素`x`推到队列的末尾 
`int pop()` 从队列的开头移除并返回元素 
`int peek()` 返回队列开头的元素 
`boolean empty()` 如果队列为空，返回`true`；否则，返回`false` 

说明： 
你只能使用标准的栈操作 —— 也就是只有`push to top`, `peek/pop from top`, `size`, 和`is empty`操作是合法的。
你所使用的语言也许不支持栈。你可以使用`list`或者`deque`（双端队列）来模拟一个栈，只要是标准的栈操作即可。 

进阶： 
你能否实现每个操作均摊时间复杂度为`O(1)`的队列？换句话说，执行`n`个操作的总时间复杂度为`O(n)`，即使其中一个操作可能花费较长时间。 

示例： 
输入：
`["MyQueue", "push", "push", "peek", "pop", "empty"]`
`[[], [1], [2], [], [], []]`
输出：
`[null, null, null, 1, 1, false]`
解释：
```java 
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
```

# 解答
```java 
import java.util.Stack;

class MyQueue {
    private Stack<Integer> stack1 = new Stack<>();
    private Stack<Integer> stack2 = new Stack<>();

    /** Initialize your data structure here. */
    public MyQueue() {

    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        stack2.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if (stack1.isEmpty()) {
            while (!stack2.isEmpty()) {
                int item = stack2.pop();
                stack1.push(item);
            }
        }
        return stack1.pop();
    }
    
    /** Get the front element. */
    public int peek() {
        if (stack1.isEmpty()) {
            while (!stack2.isEmpty()) {
                int item = stack2.pop();
                stack1.push(item);
            }
        }
        return stack1.peek();
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }
}
```
想象俩个杯子装水，只能用一个杯子喝水，只能用一个杯子倒水

---
https://leetcode-cn.com/problems/implement-queue-using-stacks/