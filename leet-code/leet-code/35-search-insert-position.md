# 题目
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。 
 你可以假设数组中无重复元素。 
示例 1: 
输入:`[1,3,5,6]`, 5
输出: 2

示例 2: 
输入:`[1,3,5,6]`, 2
输出: 1

示例 3: 
输入:`[1,3,5,6]`, 7
输出: 4

示例 4: 
输入: [1,3,5,6], 0
输出: 0

# 解答
```java 
class Solution {
    public int searchInsert(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            throw new RuntimeException("illegal parameter");
        }

        int start = 0;
        int end = nums.length - 1;

        int mid = 0;
        while (start + 1 < end) {
            mid = start + (end - start) / 2;

            if (nums[mid] > target) {
                end = mid;
            } else if (nums[mid] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }

        if (nums[start] == target) {
            return start;
        }
        if (nums[end] == target) {
            return end;
        }

        // 做找不到目标值的处理
        if (target < nums[0]) {
            return 0;
        }
        if(nums[end] < target) {
            return end + 1;
        }
        return start + 1;
    }
}
```


