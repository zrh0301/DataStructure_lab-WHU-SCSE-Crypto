# 第五周练习

**张睿恒 2024302182001**

完成题目：LeetCode167（简单），LeetCode202（简单），LeetCode49（中等），LeetCode18（中等），LeetCode36（中等），LeetCode90（困难）

## T1 LeetCode167 简单

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int l = 0;
        int r = numbers.size()-1;
        int now = numbers[l] + numbers[r];
        while(now != target){
            if(now >= target) --r;
            else ++l;
            now = numbers[l] + numbers[r];
        } 
        return {l+1,r+1};
    }
};
```

![](/home/zrheng/.config/marktext/images/2025-11-05-18-12-17-image.png)

## T2 LeetCode202 简单

```cpp
class Solution {
public:
    bool isHappy(int n) {
        int s = check(n);
        int f = check(check(n));
        while(s != f){
            s = check(s);
            f = check(check(f));
        }

        return s==1?true:false;
    }

private:
    int check(int x){
        int sum = 0;
        while(x>0){
            sum += pow(x%10,2);
            x /= 10;
        }
        return sum;
    }
};
```

![](/home/zrheng/.config/marktext/images/2025-11-05-18-21-24-image.png)

## T3 Leetcode49 中等

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector < vector <string> > ans;
        unordered_map < string , vector <string> > map1;

        for(int i=0;i<strs.size();++i){
            string key = strs[i];
            sort(key.begin(),key.end());
            map1[key].push_back(strs[i]);
        }

        for(unordered_map<string, vector<string>>::iterator it = map1.begin();it!=map1.end();++it) ans.push_back(it->second);
        

        return ans;
    }
};
```

![](/home/zrheng/.config/marktext/images/2025-11-05-18-31-13-image.png)

## T4 Leetcode18 中等

```cpp
typedef long long ll;

class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        int n = nums.size();
        set< vector <int> > uniqueRes;

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = j + 1; k < n; k++) {
                    ll sum3 = (ll)nums[i] + nums[j] + nums[k];
                    ll missing = 1ll*target - sum3;

                    for (int m = 0; m < n; m++) {
                        if (m != i && m != j && m != k && nums[m] == missing) {
                            vector <int> temp = {nums[i], nums[j], nums[k], (int)missing};
                            sort(temp.begin(), temp.end());
                            uniqueRes.insert(temp);
                            break;
                        }
                    }
                }
            }
        }

        return vector < vector <int> >(uniqueRes.begin(), uniqueRes.end());
    }
};

```

![](/home/zrheng/.config/marktext/images/2025-11-05-18-45-56-image.png)

## T5 LeetCode36 中等

```cpp
class Solution {
 public:
  bool isValidSudoku(vector < vector <char> >& board) {
    unordered_set <string> seen;

    for (int i = 0; i < 9; ++i)
      for (int j = 0; j < 9; ++j) {
        if (board[i][j] == '.') continue;
        const string c(1, board[i][j]);
        if (!seen.insert(c + "@row" + to_string(i)).second or
            !seen.insert(c + "@col" + to_string(j)).second or
            !seen.insert(c + "@box" + to_string(i/3) + to_string(j/3))
                 .second) return false;
      }

    return true;
  }
};

```

![](/home/zrheng/.config/marktext/images/2025-11-05-18-49-34-image.png)

## T6 Leetcode90 困难

```cpp
class Solution {
 public:
  vector < vector <int> > subsetsWithDup(vector <int>& nums) {
    vector < vector <int> > ans;
    ranges::sort(nums);
    dfs(nums, 0, {}, ans);
    return ans;
  }

 private:
  void dfs(const vector <int>& nums, int s, vector <int>&& path,
           vector < vector <int> >& ans) {
    ans.push_back(path);

    for (int i = s; i < nums.size(); ++i) {
      if (i > s and nums[i] == nums[i - 1]) continue;
      path.push_back(nums[i]);
      dfs(nums, i + 1, std::move(path), ans);
      path.pop_back();
    }
  }
};
```

![](/home/zrheng/.config/marktext/images/2025-11-05-19-00-21-image.png)
