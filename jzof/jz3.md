---
description: 剑指 Offer 03. 数组中重复的数字
---

# JZ3.数组中重复的数字

## 题目描述

[题目地址](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

找出数组中重复的数字。

在一个长度为 n 的数组 _`nums`_ 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

### **示例 1：**

```go
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

### **限制：**

```go
2 <= n <= 100000
```

## 题解

### 思路1 ： **哈希表 / Set**

**算法流程：**

1. 初始化： 新建 HashSet ，记为 dicdic 
2. 遍历数组 numsnums 中的每个数字 numnum 
   1. 当 num 在 dic 中，说明重复，直接返回 num 
   2. 将 numnum 添加至 dicdic 中
3. 返回 -1−1 。本题中一定有重复数字，因此这里返回多少都可以 

**复杂度分析：**

* **时间复杂度**$$O(N)$$**：**遍历数组使用 O\(N\) ，HashSet 添加与查找元素皆为 O\(1\)O\(1\) 
* **空间复杂度**$$O(N)$$**：** HashSet 占用 O\(N\) 大小的额外空间

#### 代码

{% tabs %}
{% tab title="Go" %}
```go
func findRepeatNumber2(nums []int) int {
	mapTmp := make(map[int]bool)
	for _, val := range nums {
		if mapTmp[val] {
			return val
		} else {
			mapTmp[val] = true
		}
	}
	return 0
}
```
{% endtab %}

{% tab title="Python" %}
```python
class Solution:
    def findRepeatNumber(self, nums: [int]) -> int:
        dic = set()
        for num in nums:
            if num in dic: return num
            dic.add(num)
        return -1
```
{% endtab %}

{% tab title="C++" %}
```cpp
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        unordered_map<int, bool> map;
        for(int num : nums) {
            if(map[num]) return num;
            map[num] = true;
        }
        return -1;
    }
};
```
{% endtab %}

{% tab title="Java" %}
```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> dic = new HashSet<>();
        for(int num : nums) {
            if(dic.contains(num)) return num;
            dic.add(num);
        }
        return -1;
    }
}
```
{% endtab %}
{% endtabs %}



### 思路2：**原地交换**

#### 算法流程

1. 遍历数组 numsnums ，设索引初始值为 i = 0i=0 :
   1. 若 nums\[i\] = inums\[i\]=i ： 说明此数字已在对应索引位置，无需交换，因此跳过
   2. 若 nums\[nums\[i\]\] = nums\[i\]nums\[nums\[i\]\]=nums\[i\] ： 代表索引 nums\[i\]nums\[i\] 处和索引 ii 处的元素值都为 nums\[i\]nums\[i\] ，即找到一组重复值，返回此值 nums\[i\]nums\[i\] 
   3. 否则： 交换索引为 ii 和 nums\[i\]nums\[i\] 的元素值，将此数字交换至对应索引位置
2. 若遍历完毕尚未返回，则返回 -1 

#### 复杂度分析

* **时间复杂度**$$O(N)$$**：**遍历数组使用 $$O(N)$$ ，每轮遍历的判断和交换操作使用 $$O(N)$$ 
* **空间复杂度**$$O(1)$$**：** 使用常数复杂度的额外空间。

{% tabs %}
{% tab title="Go" %}
```go
func findRepeatNumber3(nums []int) int {
	for idx, val := range nums {
		if idx == val {
			continue
		}
		if nums[val] == val {
			return val
		}
		nums[val], nums[idx] = nums[idx], nums[val]
	}
	return 0
}
```
{% endtab %}

{% tab title="Python" %}
```python
class Solution:
    def findRepeatNumber(self, nums: [int]) -> int:
        i = 0
        while i < len(nums):
            if nums[i] == i:
                i += 1
                continue
            if nums[nums[i]] == nums[i]: return nums[i]
            nums[nums[i]], nums[i] = nums[i], nums[nums[i]]
        return -1
```
{% endtab %}

{% tab title="Java" %}
```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        int i = 0;
        while(i < nums.length) {
            if(nums[i] == i) {
                i++;
                continue;
            }
            if(nums[nums[i]] == nums[i]) return nums[i];
            int tmp = nums[i];
            nums[i] = nums[tmp];
            nums[tmp] = tmp;
        }
        return -1;
    }
}
```
{% endtab %}

{% tab title="C++" %}
```cpp
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int i = 0;
        while(i < nums.size()) {
            if(nums[i] == i) {
                i++;
                continue;
            }
            if(nums[nums[i]] == nums[i])
                return nums[i];
            swap(nums[i],nums[nums[i]]);
        }
        return -1;
    }
};
```
{% endtab %}
{% endtabs %}

## 总结

如果你同我一样热爱数据结构、算法、LeetCode，可以关注我 GitHub 上的 算法 题解：[awesome-golang-algorithm](https://github.com/kylesliu/awesome-golang-algorithm)

