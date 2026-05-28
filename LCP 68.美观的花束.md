# 方法一：滑动窗口

## 解题思路

通过题意我们知道，题目要求我们维护一个窗口，使得窗口内各种数的个数不能大于cnt，并要求我们统计这种窗口的个数，这也是比较典型的滑动窗口问题

## 实现细节

1. `int left=0`用来维护区间的左边界，使的区间一直满足其中的各种元素都小于等于cnt
2. `unordered_map<int,int> mp`用来统计窗口内元素的个数，因为不要求顺序，并且好查询
3. 维护边界要用while，因为边界缩短一下不一定就满足条件
4. `ans+=i-left+1`,因为倘若一个数组满足条件，那么它的所有子数组都会满足条件

## 复杂度

- 时间复杂度:$O(n)$
- 空间复杂度:$O(n)$

## Code

```C++
class Solution {
public:
    int beautifulBouquet(vector<int>& flowers, int cnt){ 
        int n=flowers.size();
        int ans=0;
        int left=0;
        unordered_map<int,int> mp;
        for(int i=0;i<n;++i){
            mp[flowers[i]]++;
            while(mp[flowers[i]]>cnt){
                mp[flowers[left++]]--;
            }
            ans+=i-left+1;
        }
        return ans;
    }
};
```

