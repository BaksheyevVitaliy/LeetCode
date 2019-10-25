# Arrays

+ [Two Sum](#two-sum)
+ [3Sum](#3sum)
+ [Subarray Sum Equals K](#subarray-sum-equals-k)

https://leetcode.com/problems/two-sum/

## Two Sum

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> answer;
        int i, j;
        for (i = 0; i < nums.size(); ++i){
            for(j = nums.size() - 1; j > i; j--){
                if (nums[i] + nums[j] == target){
                    answer.push_back(i);
                    answer.push_back(j);
                    return answer;
                }
            }
        }
        return answer;
    }
};
```

https://leetcode.com/problems/3sum/

## 3Sum

```C++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> answer;
        int i = 0, left = 0, right = 0, buffI = 0, buffLeft = 0, buffRight = 0;
        if (nums.empty())
            return answer;
        buffI = nums[0] + 1;
        std::sort (nums.begin(), nums.end());  
        while(i < nums.size()){
            left = i + 1;
            right = nums.size() - 1;
            while(left < right){
                buffLeft = 0;
                buffRight = 0;
                if(nums[i] + nums[left] + nums[right] == 0){
                    answer.push_back(vector<int>{nums[i], nums[left], nums[right]});
                    buffLeft = 1;
                    buffRight = 1;                    
                }
                if(nums[i] + nums[left] + nums[right] > 0)
                    buffRight = 1;             
                if(nums[i] + nums[left] + nums[right] < 0)
                    buffLeft = 1;             
                if(buffLeft){
                    buffLeft = nums[left];
                    while((left < nums.size())&&(buffLeft == nums[left]))
                        left++;
                }
                if(buffRight){
                    buffRight = nums[right];
                    while((right >= 0)&&(buffRight == nums[right]))
                        right--;
                }
            } 
            buffI = nums[i];
            while((i < nums.size())&&(buffI == nums[i]))
                        i++;
            
        }
        return answer;
        
    }
};
```

https://leetcode.com/problems/subarray-sum-equals-k/

## Subarray Sum Equals K

```C++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int sum = 0, i = 0, j = 0, quantity = 0;
        for(i = 0; i < nums.size(); i++){
            sum = 0;
            for(j = i; j < nums.size(); j++){
                sum += nums[j];
                if (k == sum)
                    quantity++;
            }
        }
        return quantity;
        
    }
};
```
