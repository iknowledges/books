## 题目

给定一个整数数组nums和一个整数目标值target，请你在该数组中找出 和为目标值target的那两个整数，并返回它们的数组下标。你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。你可以按任意顺序返回答案。

**示例**：

- 输入：nums = [2,7,11,15], target = 9
- 输出：[0,1]

## 题解

1. 遍历数组nums，判断map中是否存在(target-当前值)的key。如果没有，就把当前值-下标以键值对存入map；
2. 如果有，就返回两个下标。

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> res;
        unordered_map<int, int> map;
        for (int i = 0; i < nums.size(); ++i) {
            if (map.find(target-nums[i]) == map.end()) {
                map[nums[i]] = i;
            } else {
                res.push_back(map[target-nums[i]]);
                res.push_back(i);
                break;
            }
        }
        return res;
    }
};
```
