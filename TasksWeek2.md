# 第二周练习

**张睿恒 2024302182001**

## T1 LeetCode451 中等

```cpp
class Solution {
public:
    string frequencySort(string s) {
        unordered_map<char, int> cnt;
        for (char& c : s) ++cnt[c];
        vector<char> cs;
        for (auto& [c, _] : cnt) cs.push_back(c);

        sort(cs.begin(), cs.end(), [&](char& a, char& b){
            return cnt[a] > cnt[b];
        });
        string ans;
        for (char& c : cs) ans += string(cnt[c], c);

        return ans;
    }

};
```

![](/home/zrheng/.config/marktext/images/2025-10-28-21-26-08-image.png)

## T2 LeetCode155 简单

```cpp
class MinStack {
 public:
  void push(int x) {
    if (stack.empty())
      stack.emplace(x, x);
    else
      stack.emplace(x, min(x, stack.top().second));
  }

  void pop() {
    stack.pop();
  }

  int top() {
    return stack.top().first;
  }

  int getMin() {
    return stack.top().second;
  }

 private:
  stack<pair<int, int>> stack;  // {x, min}
};
```

![](/home/zrheng/.config/marktext/images/2025-10-29-14-37-49-image.png)

## T3 LeetCode225 中等

```cpp
class MyStack {
 public:
  void push(int x) {
    q.push(x);
    for (int i = 0; i < q.size() - 1; ++i) {
      q.push(q.front());
      q.pop();
    }
  }

  int pop() {
    const int val = q.front();
    q.pop();
    return val;
  }

  int top() {
    return q.front();
  }

  bool empty() {
    return q.empty();
  }

 private:
  queue<int> q;
};
```

![](/home/zrheng/.config/marktext/images/2025-10-29-17-43-33-image.png)

## T3 LeetCode739 中等

```cpp
class Solution {
 public:
  vector<int> dailyTemperatures(vector<int>& temperatures) {
    vector<int> ans(temperatures.size());
    stack<int> stack;  // decrease stack

    for (int i = 0; i < temperatures.size(); ++i) {
      while (!stack.empty() && temperatures[stack.top()] < temperatures[i]) {
        const int index = stack.top();
        stack.pop();
        ans[index] = i - index;
      }
      stack.push(i);
    }

    return ans;
  }
};
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            
```

![](/home/zrheng/.config/marktext/images/2025-10-29-17-46-53-image.png)

## T4 LeetCode239 中等

```cpp
class Solution {
 public:
  vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector<int> ans;
    deque<int> maxQ;

    for (int i=0;i<nums.size();++i){
      while (!maxQ.empty() && maxQ.back() < nums[i]) maxQ.pop_back();
      maxQ.push_back(nums[i]);
      if (i >= k && nums[i-k] == maxQ.front()) maxQ.pop_front();
      if (i >= k-1) ans.push_back(maxQ.front());
    }

    return ans;
  }
};
```

![](/home/zrheng/.config/marktext/images/2025-10-29-17-51-47-image.png)  

## T5 LeetCode321 中等

```cpp
class Solution {
 public:
  vector <int> maxNumber(vector <int>& nums1, vector <int>& nums2, int k) {
    vector <int> ans;

    for (int k1 = 0; k1 <= k; ++k1) {
      const int k2 = k - k1;
      if (k1 > nums1.size() || k2 > nums2.size()) continue;
      ans = max(ans, merge(maxArray(nums1, k1), maxArray(nums2, k2)));
    }

    return ans;
  }

 private:
  vector <int> maxArray(const vector <int>& nums, int k) {
    vector <int> res;
    int toPop = nums.size() - k;
    for (const int num : nums) {
      while (!res.empty() && res.back() < num && toPop-- > 0) res.pop_back();
      res.push_back(num);
    }
    return {res.begin(), res.begin() + k};
  }

  // Merges nums1 and nums2.
  vector <int> merge(const vector <int>& nums1, const vector <int>& nums2) {
    vector <int> res;
    auto s1 = nums1.cbegin();
    auto s2 = nums2.cbegin();
    while (s1 != nums1.cend() or s2 != nums2.cend())
      if (lexicographical_compare(s1, nums1.cend(), s2, nums2.cend())) res.push_back(*s2++);
      else res.push_back(*s1++);
    return res;
  }
};
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            
```

![](/home/zrheng/.config/marktext/images/2025-11-12-14-10-58-image.png)

## LeetCode407 困难

```cpp
struct T {
  int i;
  int j;
  int h;  // heightMap[i][j] or the height after filling water
};

class Solution {
 public:
  int trapRainWater(vector<vector<int>>& heightMap) {
    constexpr int kDirs[4][2] = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    const int m = heightMap.size();
    const int n = heightMap[0].size();
    int ans = 0;
    auto compare = [](const T& a, const T& b) { return a.h > b.h; };
    priority_queue<T, vector<T>, decltype(compare)> minHeap(compare);
    vector<vector<bool>> seen(m, vector<bool>(n));

    for (int i = 0; i < m; ++i) {
      minHeap.emplace(i, 0, heightMap[i][0]);
      minHeap.emplace(i, n - 1, heightMap[i][n - 1]);
      seen[i][0] = true;
      seen[i][n - 1] = true;
    }

    for (int j = 1; j < n - 1; ++j) {
      minHeap.emplace(0, j, heightMap[0][j]);
      minHeap.emplace(m - 1, j, heightMap[m - 1][j]);
      seen[0][j] = true;
      seen[m - 1][j] = true;
    }

    while (!minHeap.empty()) {
      const auto [i, j, h] = minHeap.top();
      minHeap.pop();
      for (const auto& [dx, dy] : kDirs) {
        const int x = i + dx;
        const int y = j + dy;
        if (x < 0 || x == m || y < 0 || y == n)
          continue;
        if (seen[x][y])
          continue;
        if (heightMap[x][y] < h) {
          ans += h - heightMap[x][y];
          minHeap.emplace(x, y, h);  // Fill water in grid[x][y].
        } else {
          minHeap.emplace(x, y, heightMap[x][y]);
        }
        seen[x][y] = true;
      }
    }

    return ans;
  }
};
```

![](/home/zrheng/.config/marktext/images/2025-11-12-14-13-17-image.png)
