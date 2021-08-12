## 题目地址(4sum-ii/">454. 四数相加 II)

https://leetcode-cn.com/problems/4sum-ii/

## 题目描述

```
给定四个包含整数的数组列表 A , B , C , D ,计算有多少个元组 (i, j, k, l) ，使得 A[i] + B[j] + C[k] + D[l] = 0。

为了使问题简单化，所有的 A, B, C, D 具有相同的长度 N，且 0 ≤ N ≤ 500 。所有整数的范围在 -228 到 228 - 1 之间，最终结果不会超过 231 - 1 。

例如:

输入:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

输出:
2

解释:
两个元组如下:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0

```

## 思路

采用分组，HashMap记录A数组和B数组的两数之和(key)以及和的次数(value)，然后计算 C 和 D 中任意两数之和的相反数 在 hashmap 中查找是否存在 key 为 sumCD。

## 代码

- 语言支持：Java

Java Code:

```java

class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        HashMap<Integer, Integer> map = new HashMap<>();
        int res = 0;
        //统计两个数组中的元素之和，同时统计出现的次数，放入map
        for (int i : nums1) {
            for (int j : nums2) {
                int temp = i + j;
                map.put(temp, map.getOrDefault(temp,0)+1);
            }
        }
        //统计剩余的两个元素的和，在map中找是否存在相加为0的情况，同时记录次数
        for (int i : nums3) {
            for (int j : nums4) {
                int temp = i + j;
                if(map.containsKey(0 - temp)){
                    res += map.get(0 - temp);
                }
            }
        }
        return res;
    }
}

```


**复杂度分析**

令 n 为数组长度。

- 时间复杂度：$O(n^2)$，两层的for循环，哈希表的操作为O(1)
- 空间复杂度：$O(n^2)$，即为哈希映射需要使用的空间。