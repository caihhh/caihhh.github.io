---
layout: post
title: LeetCode 1 Two Sum
category: LeetCode
tags: Leetcode HashMap
description: 
---

## 题目
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,

return [0, 1].
## 思路
根据数组的内容新建一个哈希表，然后遍历数组查询哈希表中是否存在值为target-nums[i]

```
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            map.put(nums[i], i );
        }
        for(int i = 0; i < nums.length; i++){
           if(map.containsKey(target-nums[i]) && i != map.get(target-nums[i])){
                result[0] = i;
                result[1] = map.get(target-nums[i]);
                break;
            }
        }
        return result;
    }
}
```


