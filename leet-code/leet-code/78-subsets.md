
# 题目
给你一个整数数组`nums`，数组中的元素互不相同。返回该数组所有可能的子集（幂集）。 
解集不能包含重复的子集。你可以按任意顺序返回解集。 

示例 1： 
输入：`nums = [1,2,3]`
输出：`[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]`

示例 2： 
输入：`nums = [0]`
输出：`[[],[0]]`

提示： 
`1 <= nums.length <= 10` 
`-10 <= nums[i] <= 10` 
`nums`中的所有元素互不相同 

# 解答
```java 
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        if (nums.length == 0) {
            result.add(new ArrayList<>());
            return result;
        }
        List<Integer> list = new ArrayList<>();
        subsetsHelper(result, list, nums, 0);
        return result;
    }

    private void subsetsHelper(List<List<Integer>> result, List<Integer> list, int[] nums, int pos) {
        result.add(new ArrayList<>(list));

        for (int i = pos; i < nums.length; i++) {
            list.add(nums[i]);
            System.out.println(nums[i]);
            subsetsHelper(result, list, nums, i + 1);
            list.remove(list.size() - 1);
        }
        System.out.println("==子集添加结束==");
    }
}
```
使用回溯法的模版写法是：
```
1、确定最终结果
2、确定单个结果集
3、模版函数解决
4、返回
```
问题的难点就是递归辅助函数怎么写？剪枝的条件是什么？
这一题的`remove`就是回溯的关键
传入的`pos`是为了优化，减少递归子问题的规模？不是很理解

---
https://leetcode-cn.com/problems/subsets/description/