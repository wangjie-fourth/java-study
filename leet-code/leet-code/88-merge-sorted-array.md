# 题目
给你两个有序整数数组`nums1`和`nums2`，请你将`nums2`合并到`nums1`中，使`nums1`成为一个有序数组。 
初始化`nums1`和`nums2`的元素数量分别为`m`和`n`。你可以假设`nums1`的空间大小等于`m + n`，这样它就有足够的空间保存来自`nums2`的元素。 
示例 1： 
输入：`nums1 = [1,2,3,0,0,0]`, `m = 3`, `nums2 = [2,5,6]`, `n = 3`
输出：`[1,2,2,3,5,6]`
示例 2： 
输入：`nums1 = [1]`, `m = 1`, `nums2 = []`, `n = 0`
输出：`[1]`

# 解答
```java 
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int nums1Index = 0;
        int nums2Index = 0;
        int index = 0;

        // 为了防止后面连续移动nums1元素，这里腾出nums1数组
        int[] tempNums = new int[m];
        for (int i = 0; i < m; i++) {
            tempNums[i] = nums1[i];
        }

        while (nums1Index < tempNums.length && nums2Index < nums2.length) {
            if (tempNums[nums1Index] > nums2[nums2Index]) {
                nums1[index] = nums2[nums2Index];
                nums2Index++;
            } else {
                nums1[index] = tempNums[nums1Index];
                nums1Index++;
            }
            index++;
        }

        // 如果其中一个数组未完全移动完
        for (int i = nums1Index; i < tempNums.length; i++) {
            nums1[index] = tempNums[i];
            index++;
        }
        for (int i = nums2Index; i < nums2.length; i++) {
            nums1[index] = nums2[i];
            index++;
        }
    }
}
```
这也是**双指针**思路解法的题目

https://leetcode-cn.com/problems/merge-sorted-array/