# Intervals

+ [Non-overlapping Intervals](#non-overlapping-intervals)
+ [Merge Intervals](#merge-intervals)
+ [Insert Interval](#insert-interval)

https://leetcode.com/problems/non-overlapping-intervals/

## Non-overlapping Intervals

```C++
bool myfunction(vector<int>& a, vector<int>& b) {
    return (a[0] < b[0]);
}
class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        int answer = 0, i = 0, j = 1;
        if (intervals.empty())
            return answer;
        sort (intervals.begin(), intervals.end(), myfunction);
        while(j < intervals.size()){
            if(intervals[i][1] > intervals[j][0]){
                answer++;
                if(intervals[i][1] > intervals[j][1])
                    i = j;                
            }
            else
                i = j;
            j++;
        }
        return answer;        
    }    
};
```

https://leetcode.com/problems/merge-intervals/

## Merge Intervals

```C++
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        vector<vector<int>> answer;
        vector<int> start, finish;
        int i = 0, j = -1, leftPoint = 0, rightPoint = 0, sumOfStartsPointsMinusEndPoints = 0;
        if (intervals.empty())
            return answer;
        while(++j < intervals.size()){
            start.push_back(intervals[j][0]);
            finish.push_back(intervals[j][1]);            
        }
        sort(start.begin(), start.end());
        sort(finish.begin(), finish.end());
        j = 0;
        while(j < intervals.size()){
            leftPoint = i++;
            sumOfStartsPointsMinusEndPoints = 1;
            while(sumOfStartsPointsMinusEndPoints){
                if((i != intervals.size())&&(start[i]<= finish[j])){
                    sumOfStartsPointsMinusEndPoints++;
                    i++;
                }
                else{
                    sumOfStartsPointsMinusEndPoints--;
                    j++;
                }
            }
            rightPoint = j - 1;
            answer.push_back(vector<int>{start[leftPoint], finish[rightPoint]});
        }
        return answer;        
    }    
};
```

https://leetcode.com/problems/insert-interval/

## Insert Interval

```C++
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> answer;
        vector<int> start, finish;
        int i = 0, j = -1, leftPoint = 0, rightPoint = 0, sumOfStartsPointsMinusEndPoints = 0;
        if (intervals.empty()){
             answer.push_back(newInterval);
            return answer;
        }
        while(++j < intervals.size()){
            start.push_back(intervals[j][0]);
            finish.push_back(intervals[j][1]);            
        }
        start.push_back(newInterval[0]);
        finish.push_back(newInterval[1]);    
        sort(start.begin(), start.end());
        sort(finish.begin(), finish.end());
        j = 0;
        while(j < finish.size()){
            leftPoint = i++;
            sumOfStartsPointsMinusEndPoints = 1;
            while(sumOfStartsPointsMinusEndPoints){
                if((i != start.size())&&(start[i]<= finish[j])){
                    sumOfStartsPointsMinusEndPoints++;
                    i++;
                }
                else{
                    sumOfStartsPointsMinusEndPoints--;
                    j++;
                }
            }
            rightPoint = j - 1;
            answer.push_back(vector<int>{start[leftPoint], finish[rightPoint]});
        }
        return answer;        
    }    
};
```
