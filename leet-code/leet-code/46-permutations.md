# 题目
给定一个没有重复数字的序列，返回其所有可能的全排列。 

示例: 
输入: `[1,2,3]`
输出:
`[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]` 

# 解答
```java 
import java.util.ArrayList;
import java.util.List;

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        if (nums.length == 0 ) {
            return result;
        }

        List<Integer> list = new ArrayList<>();
        permuteHelper(result, list, nums);
        return result;
    }

    private void permuteHelper(List<List<Integer>> result, List<Integer> list, int[] nums) {
        if (nums.length == list.size()) {
            result.add(new ArrayList<>(list));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            if (list.contains(nums[i])) {
                continue;
            }
            list.add(nums[i]);
            permuteHelper(result, list, nums);
            list.remove(list.size() - 1);
        }
    }
}
```




---
https://leetcode-cn.com/problems/permutations/
