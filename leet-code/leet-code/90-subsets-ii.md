
# 题目
给定一个可能包含重复元素的整数数组`nums`，返回该数组所有可能的子集（幂集）。 
说明：解集不能包含重复的子集。 

示例: 
输入: `[1,2,2]`
输出:
`[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]` 

# 解答
```java 
import java.util.Arrays;
import java.util.List;
import java.util.ArrayList;

class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        if (nums.length == 0) {
            result.add(new ArrayList<>());
            return result;
        }

        Arrays.sort(nums);
        List<Integer> list = new ArrayList<>();
        subsetsWithDupHelper(result, list, nums, 0);
        return result;
    }

    private void subsetsWithDupHelper(List<List<Integer>> result, List<Integer> list, int[] nums, int pos) {
        result.add(new ArrayList<>(list));


        for (int i = pos; i < nums.length; i++) {
            if (i != pos && nums[i] == nums[i - 1]) {
                continue;
            }
            list.add(nums[i]);
            subsetsWithDupHelper(result, list, nums, i + 1);
            list.remove(list.size() - 1);
        }
    }
}
```
虽然模版很一样，但是理解起来有点麻烦。


---
https://leetcode-cn.com/problems/subsets-ii/description/
