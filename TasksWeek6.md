# 第六周练习

**张睿恒 2024302182001**

完成题目：LeetCode215 简单

## T1 LeetCode215

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue <int,vector <int>,greater <> > que;
        for(int i=0;i<nums.size();++i){
            que.push(nums[i]);
            if(que.size() > k) que.pop();
        }

        return que.top();
    }
};
```

![](/home/zrheng/.config/marktext/images/2025-11-12-17-00-50-image.png)

## T2 LeetCode347

```cpp
struct T{
    int num,freq;
};


class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        int n = nums.size();
        vector <int> ans;
        unordered_map <int,int> cnt;
        auto cmp = [](const T& a,const T& b){return a.freq > b.freq;};
        priority_queue <T, vector <T>, decltype(cmp)> que(cmp);

        for(int i=0;i<n;++i){
            cnt[nums[i]]++;
        }
        for (const auto& [num, freq] : cnt) {
            que.emplace(num, freq);
            if (que.size() > k) que.pop();
        }

        while (!que.empty())
            ans.push_back(que.top().num), que.pop();

        return ans;        
    }
};
```

![](/home/zrheng/.config/marktext/images/2025-11-12-17-16-07-image.png)


