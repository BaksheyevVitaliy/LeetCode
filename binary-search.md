# Binary search

+ [Binary Search](#binary-search)
+ [Search in Rotated Sorted Array](#search-in-rotated-sorted-array)
+ [Find Minimum in Rotated Sorted Array](#find-minimum-in-rotated-sorted-array)
+ [Find K Closest Elements](#find-k-closest-elements/submissions)

https://leetcode.com/problems/binary-search/

## Binary Search

```C++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int size = nums.size();
        if (size == 0)
            return -1;
        int lptr = 0;
        int rptr = size - 1;
        while(lptr <= rptr){
            int med = floor((lptr + rptr) / 2);        
        if (nums[med] == target)
            return med;
        if (nums[lptr] == target)
            return lptr;
        if (nums[rptr] == target)
            return rptr;
        if (rptr -lptr <=1)
            return -1;
        else{
            if (nums[med] < target) {
                lptr = med;
            }
            else{
                rptr = med;
            }
        }
        
    }
    return -1;
    
    
}
};
```

https://leetcode.com/problems/search-in-rotated-sorted-array/

## Search in Rotated Sorted Array

```C++
class Solution {
    int findMin(vector<int>& nums) {
        int left = -1;
        int right = nums.size() - 1;
        while (left < right - 1) {
            int mid = (left + right) / 2;
            if (nums[mid] < nums[right])
                right = mid;
            else
                left = mid;
        }
        return right;
  }
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        if(nums.size() == 0)
            return -1;
        if(nums[right] >= target)
            left = findMin(nums);
        else
            right = findMin(nums) - 1;
        while(left <= right){
            int med = floor((left + right) / 2);        
        if (nums[med] == target)
            return med;
        if (nums[left] == target)
            return left;
        if (nums[right] == target)
            return right;
        if (right -left <=1)
            return -1;
        else{
            if (nums[med] < target) {
                left = med;
            }
            else{
                right = med;
            }
        }
        
    }
    return -1;
    }
};
```

https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/

## Find Minimum in Rotated Sorted Array

```C++
class Solution {
 public:
  int findMin(vector<int>& nums) {
    int left = -1;
    int right = nums.size() - 1;
    while (left < right - 1) {
      int mid = (left + right) / 2;
      if (nums[mid] < nums[right])
        right = mid;
      else
        left = mid;
    }
    return nums[right];
  }
};
```

https://leetcode.com/problems/find-k-closest-elements/

## Find K Closest Elements

```C++
class Solution {
 public:
  vector<int> findClosestElements(vector<int>& arr, int k, int x) {
    int left = 0, right = arr.size() - k;
    while (left < right) {
      int mid = (left + right) / 2;
      if (x - arr[mid] > arr[mid + k] - x)
        left = mid + 1;
      else
        right = mid;
    }
    return vector<int>(arr.begin() + left, arr.begin() + left + k);
  }
};
```
