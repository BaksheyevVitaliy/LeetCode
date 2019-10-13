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
        vector <int> result(0);
        map <int, int> NewNums;
        for (int i = 0; i < nums.size(); i++)
                NewNums[nums[i]] = i;
        for (int i = 0; i < NewNums.size(); i++){
            if((NewNums.find(target - nums[i]) != NewNums.end())&&(NewNums[target - nums[i]] != i)){
                result.push_back(i);
                result.push_back(NewNums[target - nums[i]]);
                break;
            }
        }
        return result;
    }
};
```

https://leetcode.com/problems/3sum/

## 3Sum

```C++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> Answer;
        int i = 0, left = 0, right = 0, buffi = 0, buffleft = 0, buffright = 0;
        if (nums.empty())
            return Answer;
        buffi = nums[0] + 1;
        std::sort (nums.begin(), nums.end());  
        while(i < nums.size()){
            left = i + 1;
            right = nums.size() - 1;
            while(left < right){
                buffleft = 0;
                buffright = 0;
                if(nums[i] + nums[left] + nums[right] == 0){
                    Answer.push_back(vector<int>{nums[i], nums[left], nums[right]});
                    buffleft = 1;
                    buffright = 1;                    
                }
                if(nums[i] + nums[left] + nums[right] > 0)
                    buffright = 1;             
                if(nums[i] + nums[left] + nums[right] < 0)
                    buffleft = 1;             
                if(buffleft){
                    buffleft = nums[left];
                    while((left < nums.size())&&(buffleft == nums[left]))
                        left++;
                }
                if(buffright){
                    buffright = nums[right];
                    while((right >= 0)&&(buffright == nums[right]))
                        right--;
                }
            } 
            buffi = nums[i];
            while((i < nums.size())&&(buffi == nums[i]))
                        i++;
            
        }
        return Answer;
        
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
                sum = sum + nums[j];
                if (k == sum)
                    quantity++;
            }
        }
        return quantity;
        
    }
};
```
