# 题目
编写一个高效的算法来判断`m x n`矩阵中，是否存在一个目标值。该矩阵具有如下特性： 
每行中的整数从左到右按升序排列。 
每行的第一个整数大于前一行的最后一个整数。 

示例 1： 
输入：`matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]]`, `target = 3`
输出：`true`

示例 2： 
输入：`matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]]`, `target = 13`
输出：`false`

提示： 
`m == matrix.length`
`n == matrix[i].length` 
`1 <= m, n <= 100`
`-104 <= matrix[i][j], target <= 104`

# 解答
1、在行、列做俩次二分查找
```java 
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0) {
            throw new RuntimeException("illegle input params");
        }

        // 确定target在哪一维数组里
        int start = 0;
        int end = matrix.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (matrix[mid][0] > target) {
                end = mid;
            } else if (matrix[mid][0] < target) {
                start = mid;
            } else {
                start = mid;
            }
        }
        if (matrix[start][0] == target) {
            return true;
        }
        if (matrix[end][0] == target) {
            return true;
        }


        if (matrix[start][0] > target) {
            return false;
        }
        /* 注意：下面俩个不能调整位置 */
        // 就在start那一维查找
        System.out.println("在维度为" + start + "中查找");
        if (searchMatrix(matrix[start], target)) {
            return true;
        }
        // 在最后一维数组中查找
        System.out.println("在维度为" + (matrix.length - 1) + "中查找");
        return searchMatrix(matrix[matrix.length - 1], target);
    }

    public boolean searchMatrix(int[] matrix, int target) {
        if (matrix == null || matrix.length == 0) {
            throw new RuntimeException("illegle input params");
        }

        int start = 0;
        int end = matrix.length - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            if (matrix[mid] > target) {
                end = mid;
            } else if (matrix[mid] < target) {
                start = mid;
            } else {
                start = mid;
            }
        }
        if (matrix[start] == target) {
            return true;
        }
        if (matrix[end] == target) {
            return true;
        }
        return false;
    }


}
```

2、把二维降成一维
要掌握二维变一维的下标转换
```java 
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0) {
            throw new RuntimeException("illegle input params");
        }

        int row = matrix.length;
        int col = matrix[0].length;

        int start = 0;
        int end = row * col - 1;
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            int firstIndex = mid / col;
            int secondIndex = mid % col;

            if (matrix[firstIndex][secondIndex] > target) {
                end = mid;
            } else if (matrix[firstIndex][secondIndex] < target) {
                start = mid;
            } else {
                end = mid;
            }
        }
        
        if (matrix[start / col][start % col] == target) {
            return true;
        }
        if (matrix[end / col][end % col] == target) {
            return true;
        }
        return false;
    }
}
```


