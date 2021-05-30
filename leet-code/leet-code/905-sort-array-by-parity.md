
# 题目
给定一个非负整数数组 A，返回一个数组，在该数组中， A 的所有偶数元素之后跟着所有奇数元素。 
你可以返回满足此条件的任何数组作为答案。 
示例： 
输入：`[3,1,2,4]`
输出：`[2,4,3,1]`、`[4,2,3,1]`、`[2,4,1,3]`、`[4,2,1,3]` 

# 解法
```java 
class Solution {
    public int[] sortArrayByParity(int[] A) {
        int begin = 0;
        int end = A.length - 1;
        while (begin < end) {
            if (A[begin] % 2 != 0) {
                int temp = A[begin];
                A[begin] = A[end];
                A[end] = temp;
                end--;
            } else {
                begin++;
            }
        }
        return A;
    }
}
```
这也是**双指针**思路的解法


---
https://leetcode-cn.com/problems/sort-array-by-parity/