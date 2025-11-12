# 第一周练习

**张睿恒 2024302182001**

## T1 LeetCode1 简单

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        for(int i=0;i<n;++i){
            for(int j=i+1;j<n;++j){
                if(nums[i] + nums[j] == target) return {i,j};
            }
        }
        return {};
    }

};
```

![](/home/zrheng/.config/marktext/images/2025-10-11-18-39-52-image.png)

## T2 LeetCode27 简单

```cpp
class Solution {
 public:
  int removeElement(vector<int>& nums, int val) {
    int i = 0;

    for (const int num : nums)
      if (num != val)
        nums[i++] = num;

    return i;
  }
};
```

![](/home/zrheng/.config/marktext/images/2025-10-11-19-15-42-image.png)

## T3 LeetCode206 中等

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head == NULL or head->next == NULL) return head;
        ListNode* newHead = reverseList(head->next);
        head->next->next = head;
        head->next = NULL;
        return newHead;
    }
};
```

![](/home/zrheng/.config/marktext/images/2025-10-11-19-20-10-image.png)

## T5 LeetCode21 中等

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        if(list1 == NULL or list2 == NULL) return list1 ? list1 : list2;
        if(list1->val > list2->val) swap(list1 , list2);
        list1->next = mergeTwoLists(list1->next , list2);
        return list1;
    }
};
```

![](/home/zrheng/.config/marktext/images/2025-10-11-19-28-37-image.png)

## T7 LeetCode42 困难

```cpp
class Solution {
 public:
  int trap(vector<int>& height) {
    const int n = height.size();
    int ans = 0;
    vector<int> l(n);  
    vector<int> r(n);  

    l[0] = height[0];
    r[n-1] = height[n-1];
    for (int i = 1; i < n; ++i)
      l[i] = max(height[i], l[i - 1]);

    for (int i = n - 2; i >= 0; --i)
      r[i] = max(height[i], r[i + 1]);

    for (int i = 0; i < n; ++i)
      ans += min(l[i], r[i]) - height[i];

    return ans;
  }
};
```

![](/home/zrheng/.config/marktext/images/2025-10-11-20-05-12-image.png)

## T8 LeetCode322 困难

```cpp
class Solution {
 public:
  int coinChange(vector<int>& coins, int amount) {

    vector<int> dp(amount + 1, amount + 1);
    dp[0] = 0;

    for (int i=1;i<=amount;++i)
      for (const int coin : coins)
        if (coin <= i) dp[i] = min(dp[i],dp[i-coin]+1);

    if(dp[amount] == amount+1) return -1;
    return dp[amount];
  }
};
```

![](/home/zrheng/.config/marktext/images/2025-10-11-20-34-17-image.png)
