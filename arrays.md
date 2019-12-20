# Arrays

+ [Two Sum](#two-sum)
+ [3Sum](#3sum)
+ [Subarray Sum Equals K](#subarray-sum-equals-k)
+ [Maximum Subarray](#maximum-subarray)
+ [Maximum Product Subarray](#maximum-product-subarray)

https://leetcode.com/problems/two-sum/

## Two Sum

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> answer;
        for (int i = 0; i < nums.size(); ++i){
            for(int j = nums.size() - 1; j > i; j--){
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
        int sum = 0, quantity = 0;
        for(int i = 0; i < nums.size(); i++){
            sum = 0;
            for(int j = i; j < nums.size(); j++){
                sum += nums[j];
                if (k == sum)
                    quantity++;
            }
        }
        return quantity;
        
    }
};
```

https://leetcode.com/problems/maximum-subarray/

## Maximum Subarray

```C++
class Solution {
 public:
  int maxSubArray(vector<int>& nums) {
    int currMaxSum = nums[0], res = nums[0];
    for (int i = 1; i < nums.size(); i++) {
      if (currMaxSum < 0)
        currMaxSum = nums[i];
      else
        currMaxSum += nums[i];
      res = max(res, currMaxSum);
    }
    return res;
  }
};
```

https://leetcode.com/problems/maximum-product-subarray/

## Maximum Product Subarray

```C++
class Solution {
 public:
  int maxProduct(vector<int>& nums) {
    int leftProduct = 0, rightProduct = 0;
    int res = nums[0];
    int size = nums.size();
    for (int i = 0; i < size; i++) {
      if (leftProduct != 0) {
        leftProduct *= nums[i];
      } else {
        leftProduct = nums[i];
      }
      if (rightProduct != 0) {
        rightProduct *= nums[size - i - 1];
      } else {
        rightProduct = nums[size - i - 1];
      }
      res = max(res, max(leftProduct, rightProduct));
    }
    return res;
  }
};
```
