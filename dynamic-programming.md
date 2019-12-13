# Dynamic programming

+ [Knapsack problem](#knapsack-problem)
+ [Climbing Stairs](#climbing-stairs)
+ [Longest Increasing Subsequence](#longest-increasing-subsequence)
+ [Coin Change](#coin-change)
+ [Coin Change 2](#coin-change-2)
+ [House Robber](#house-robber)
+ [House Robber II](#house-robber-ii)
+ [Jump Game](#jump-game)
+ [Jump Game II](#jump-game-ii)
+ [Decode Ways](#decode-ways)
+ [Unique Paths](#unique-paths)
+ [Unique Paths II](#unique-paths-ii)
+ [Longest Common Subsequence](#longest-common-subsequence)
+ [Word Break](#word-break)
+ [N-Queens](#n-queens)
+ [N-Queens II](#n-queens-ii)

## Knapsack problem

https://stepik.org/lesson/13259/step/5?unit=3444

```C++

int MaxWeight(int capacity, vector<int>& nums) {
  vector<vector<int>> maxValue(nums.size() + 1, vector<int>(capacity + 1));
  for (int i = 1; i <= nums.size(); i++) {
    for (int j = 1; j <= capacity; j++) {
      if (nums[i - 1] > j)
        maxValue[i][j] = maxValue[i - 1][j];
      else
        maxValue[i][j] = max(maxValue[i - 1][j],
                              maxValue[i - 1][j - nums[i - 1]] + nums[i - 1]);
    }
  }
  return maxValue.back().back();
}
```

## Climbing Stairs

https://leetcode.com/problems/climbing-stairs/

```C++
class Solution {
public:
    int climbStairs(int n) {
        int first = 0, last = 1, i;
        for(i = 0; i < n; i++){
            last += first;
            first = last - first;
        }
        return last;
    }
};
```

## Longest Increasing Subsequence

https://leetcode.com/problems/longest-increasing-subsequence/

```C++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        vector<int> subsequence;
        int answer = 0;
        int bufnumber = 0;
        for(int i = 0; i < nums.size(); i++){
            bufnumber = 0;
            for(int j = i; j >= 0; j--){
                if((nums[i] > nums[j])&&(bufnumber < subsequence[j])){
                    bufnumber = subsequence[j];
                }
            }
            subsequence.push_back(bufnumber + 1);
            if(subsequence[i] > answer)
                answer = subsequence[i];
        }
        return answer;
    }
};
```

## Coin Change

https://leetcode.com/problems/coin-change/

```C++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> minForSum(amount + 1, amount + 1);
        int i, j;
        minForSum[0] = 0;
        for(i = 0; i < coins.size(); i++){
            for(j = coins[i]; j < amount + 1; j++){
                if(minForSum[j - coins[i]] < minForSum[j])
                    minForSum[j] = minForSum[j - coins[i]] + 1;
            }
        }
        if(minForSum[amount] != (amount + 1))
            return minForSum[amount];
        return -1;
    }
};
```

## Coin Change 2

https://leetcode.com/problems/coin-change-2/

```C++
class Solution {
public:
    int change(int amount, vector<int>& coins) {
      vector<int> minForSum(amount + 1, 0);
        int i, j;
        minForSum[0] = 1;
        for(i = 0; i < coins.size(); i++){
            for(j = coins[i]; j < amount + 1; j++){
                minForSum[j] += minForSum[j - coins[i]];
            }
        }
        return minForSum[amount];
    }
};
```

## House Robber

https://leetcode.com/problems/house-robber/

```C++
class Solution {
public:
    int rob(vector<int>& nums) {
        int prev = 0;
        int predPrev = 0;
        int current = 0;
        if(nums.size() == 0)
            return 0;
        prev = nums[0];
      for (int i = 1; i < nums.size(); i++) {
          current = max(prev, predPrev + nums[i]);
          predPrev = prev;
          prev = current;
      }
    return prev;
    }
};
```

## House Robber II

https://leetcode.com/problems/house-robber-ii/

```C++
class Solution {
public:
    int rob(vector<int>& nums) {
        int prev = 0;
        int predPrev = 0;
        int current = 0;
        int prev1 = 0;
        if(nums.size() == 0)
            return 0;
        if(nums.size() == 1)
            return nums[0];
        prev = nums[0];
      for (int i = 1; i < nums.size() - 1; i++) {
          current = max(prev, predPrev + nums[i]);
          predPrev = prev;
          prev = current;
      }
        prev1 = nums[1];
        predPrev = 0;
      for (int i = 2; i < nums.size(); i++) {
          current = max(prev1, predPrev + nums[i]);
          predPrev = prev1;
          prev1 = current;
      }
    return max(prev,prev1);   
    }
};
```

## Jump Game

https://leetcode.com/problems/jump-game/

```C++
class Solution {
public:
    bool canJump(vector<int>& nums) {
      int maxBound = 0;
      for (int i = 0; i < nums.size() - 1; i++) {
        if ((i + nums[i] > maxBound)&&(i <= maxBound)){
          maxBound = i + nums[i];
        }
      }
      return maxBound >= nums.size() - 1;
    }
};
```

## Jump Game II

https://leetcode.com/problems/jump-game-ii/

```C++
class Solution {
public:
    int jump(vector<int>& nums) {
        int maxBound = 0;
        int currJump = 0;
        int numberJump = 0;
        for (int i = 0; i < nums.size() - 1; i++) {
            if (i + nums[i] > maxBound){
                maxBound = i + nums[i];
            }
            if(i == currJump){
                currJump = maxBound;
                numberJump++;
            }
        }
        return numberJump;       
    }
};
```

## Decode Ways

https://leetcode.com/problems/decode-ways/

```C++
class Solution {
 public:
  int numDecodings(string s) {
    int tmp;
    int prev = 0, cur = 1;
    for (int i = 0; i < s.length(); i++) {
      if (s[i] == '0') 
          cur = 0;
      tmp = cur + prev;
      if (!cur && !prev) 
          return 0;
      if ((s[i] == '1') || (s[i] == '2') && (s[i + 1] <= '6'))
        prev = cur;
      else
        prev = 0;
      cur = tmp;
    }
    return cur;
  }
};
```

## Unique Paths

https://leetcode.com/problems/unique-paths/

```C++
class Solution {
public:
    int uniquePaths(int m, int n) {
        int map[m][n];
        map[0][0] = 1;
        for(int i = 0; i < m; i++)
            for(int j = 0 + (i == 0); j < n; j++){
                map[i][j] = 0;
                if(i > 0)
                    map[i][j] += map[i-1][j];
                if(j > 0)
                    map[i][j] += map[i][j-1];
            }
        return map[m-1][n-1];
    }
};
```

## Unique Paths II

https://leetcode.com/problems/unique-paths-ii/

```C++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int sizeh = obstacleGrid.size();
        int sizew = obstacleGrid[0].size();
        vector<long> Counter(sizew);  
        if(obstacleGrid[0][0] == 1)
            return 0;
        Counter[0] = 1;
        for(int i = 0; i < obstacleGrid.size();i++){
            for(int j = 0; j < sizew; j++){
                if(obstacleGrid[i][j] == 1)
                    Counter[j] = 0;
                else{
                    if(j > 0)
                        Counter[j] += Counter[j - 1];
                }
            }
        }
        return Counter[sizew - 1];
    }
};
```

## Longest Common Subsequence

https://leetcode.com/problems/longest-common-subsequence/

```C++
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int l1 = text1.length();
        int l2 = text2.length();
        int maximum = 0;
        vector<int> longest(l2, 0);
        vector<int> buff(l2, 0);
        for(int i = 0; i < text1.length(); i++){
            maximum = 0;
            for(int j = 0; j < text2.length(); j++){
                if(text2[j] == text1[i])
                    buff[j] = max(maximum + 1, longest[j]);
                maximum = max(maximum,longest[j]);
            }
            for(int j = 0; j < text2.length(); j++){
                if(buff[j] != 0){
                    longest[j] = buff[j];
                    buff[j] = 0;
                }
            }
        }
        for(int j = 0; j < text2.length(); j++){
                maximum = max(maximum,longest[j]);
            }
        return maximum;
    }
};
```

## Word Break

https://leetcode.com/problems/word-break/

```C++
class Solution {
 public:
  bool wordBreak(string s, vector<string>& wordDict) {
    unordered_set<string> wordSet(wordDict.begin(), wordDict.end());
    unordered_map<string, bool> memo;
    return wordBreakHelp(s, wordSet, memo);
  }
  bool wordBreakHelp(string& s, unordered_set<string>& wordSet,
                     unordered_map<string, bool>& memo) {
    if (memo.find(s) != memo.end()) return memo[s];
    if (wordSet.find(s) != wordSet.end()) return memo[s] = true;
    for (int i = 1; i < s.size(); i++) {
      string rightPart = s.substr(i);
      if (wordSet.find(rightPart) == wordSet.end()) continue;
      string leftPart = s.substr(0, i);
      if (wordBreakHelp(leftPart, wordSet, memo)) return memo[s] = true;
    }
    return memo[s] = false;
  }
};
```

## N-Queens

https://leetcode.com/problems/n-queens/

```C++
class Solution {
private:
public:
    void SearchSolution(int column, int n, vector<string>& currRes,
                        vector<int>& Line, vector<int>& RDiag,
                        vector<int>& LDiag, vector<vector<string>>& res) {
      if (column == n)
        res.push_back(currRes);
      else {
        for (int row = 0; row < n; row++) {
          if ((Line[row] == 0) && (RDiag[row + column] == 0)
             && (LDiag[column - row + n - 1] == 0)) {
            currRes[row][column] = 'Q';
            Line[row] = 1;
            RDiag[row + column] = 1;
            LDiag[column - row + n - 1] = 1;
            SearchSolution(column + 1, n, currRes, Line, RDiag, LDiag, res);
            currRes[row][column] = '.';
            Line[row] = 0;
            RDiag[row + column] = 0;
            LDiag[column - row + n - 1] = 0;
          }
        }
      }
    }
    vector<vector<string>> solveNQueens(int n) {
      vector<vector<string>> res;
      vector<int> Line(n, 0);
      vector<int> RDiag(2 * n - 1, 0);
      vector<int> LDiag(2 * n - 1, 0);
      vector<string> currRes(n, string (n, '.'));
      SearchSolution(0, n, currRes, Line, RDiag, LDiag, res);
      return res;
    }
};
```

## N-Queens II

https://leetcode.com/problems/n-queens-ii/

```C++
class Solution {
public:
    void SearchSolution(int column, int n, vector<int>& Line,
                        vector<int>& RDiag, vector<int>& LDiag,
                        vector<int>& res) {
      if (column == n)
        res[0]++;
      else {
        for (int row = 0; row < n; row++) {
          if ((Line[row] == 0) && (RDiag[row + column] == 0)
             && (LDiag[column - row + n - 1] == 0)) {
            Line[row] = 1;
            RDiag[row + column] = 1;
            LDiag[column - row + n - 1] = 1;
            SearchSolution(column + 1, n, Line, RDiag, LDiag, res);
            Line[row] = 0;
            RDiag[row + column] = 0;
            LDiag[column - row + n - 1] = 0;
          }
        }
      }
    }
    int totalNQueens(int n) {
      vector<int> res(1,0);
      vector<int> Line(n, 0);
      vector<int> RDiag(2 * n - 1, 0);
      vector<int> LDiag(2 * n - 1, 0);
      SearchSolution(0, n, Line, RDiag, LDiag, res);
      return res[0];
        
    }
};
```
