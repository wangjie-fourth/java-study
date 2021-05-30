
用于在排序的集合中查找某个元素。只不过需要注意一些细节。

# 模版
```java 
    public int binarySearch(int[] nums, int target) {
        if (nums == null || nums.length == 0) {
            return -1;
        }

        int start = 0;
        int end = nums.length - 1;

        while (start + 1 < end) { // （1）防止死循环
            int mid = start + (end - start) / 2; // (2)防止数据溢出
            if (target < nums[mid]) {
                end = mid;
            } else if (target > nums[mid]) {
                start = mid;
            } else {
                end = mid; // （3）方便获取第一个出现的值
            }
        }

        if (nums[start] == target) {
            return start;
        }
        if (nums[end] == target) {
            return end;
        }
        return -1;
    }
```
1、为什么循环条件和循环体写成这样？



# 相关题目
https://leetcode-cn.com/problems/first-bad-version/description/

https://leetcode.com/problems/search-insert-position/description/

https://leetcode-cn.com/problems/search-a-2d-matrix/description/

https://leetcode-cn.com/problems/search-a-2d-matrix-ii/description/

https://leetcode-cn.com/problems/sqrtx/description/

https://leetcode-cn.com/problems/search-in-rotated-sorted-array/description/


