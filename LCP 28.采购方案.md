# 方法一：双指针

## 解题思路

因为统计时与大小有关系，而原数组是无序的，所以我们如果要统计两个值的和小于target的数据对的个数，最简单的办法就是用两层循环把每一种情况都枚举出来，实现比较简单，而我们想要优化，就是**将数组排序**，排序后**分别设置在数组的两端**，**在二者和大于target的时候，移动右指针直到和小于等于target**这时因为非递减排列**左指针和两指针区间任何一个数相加都小于等于target**，数量直接加`right-target`个，然后**移动左指针**，每移动一步就**重复一遍上述操作**

当**两指针相遇时结束**即可

> 1e9+7是double类型
>
> `1e9+6` 被判定为 `double` 类型，是因为在 C++ 中，**科学计数法（如 `1e9`）本身就是浮点数字面量**。无论它的值看起来多像整数，只要用了 `e` 或 `E` 的格式，编译器就会把它当作 `double`。这是 C++ 语法层面的规定，与它能否放进 `int` 无关。

## 复杂度

- 时间复杂度:$O(n)$
- 空间复杂度:$O(1)$

## Code

```C++
class Solution {
public:
    int purchasePlans(vector<int>& nums, int target) {
        sort(nums.begin(),nums.end());
        int n=nums.size();
        int left=0;
        int right=n-1;
        int ans=0;
        while(left<right){
            if(nums[left]+nums[right]<=target){
                ans+=right-left;
                ans%=(int)1e9+7;
                left++;
            }else{
                right--;
            }
        }
        return ans;
    }
};
```

