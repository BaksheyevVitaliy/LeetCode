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
        vector<vector<int>> Answer;
        vector<int> start, finish;
        int i = 0, j = -1, LeftPoint = 0, RightPoint = 0, SumOfStartsPointsMinusEndPoints = 0;
        if (intervals.empty())
            return Answer;
        while(++j < intervals.size()){
            start.push_back(intervals[j][0]);
            finish.push_back(intervals[j][1]);            
        }
        sort(start.begin(), start.end());
        sort(finish.begin(), finish.end());
        j = 0;
        while(j < intervals.size()){
            LeftPoint = i++;
            SumOfStartsPointsMinusEndPoints = 1;
            while(SumOfStartsPointsMinusEndPoints){
                if((i != intervals.size())&&(start[i]<= finish[j])){
                    SumOfStartsPointsMinusEndPoints++;
                    i++;
                }
                else{
                    SumOfStartsPointsMinusEndPoints--;
                    j++;
                }
            }
            RightPoint = j - 1;
            Answer.push_back(vector<int>{start[LeftPoint], finish[RightPoint]});
        }
        return Answer;        
    }    
};
```

https://leetcode.com/problems/insert-interval/

## Insert Interval

```C++
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> Answer;
        vector<int> start, finish;
        int i = 0, j = -1, LeftPoint = 0, RightPoint = 0, SumOfStartsPointsMinusEndPoints = 0;
        if (intervals.empty()){
             Answer.push_back(newInterval);
            return Answer;
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
            LeftPoint = i++;
            SumOfStartsPointsMinusEndPoints = 1;
            while(SumOfStartsPointsMinusEndPoints){
                if((i != start.size())&&(start[i]<= finish[j])){
                    SumOfStartsPointsMinusEndPoints++;
                    i++;
                }
                else{
                    SumOfStartsPointsMinusEndPoints--;
                    j++;
                }
            }
            RightPoint = j - 1;
            Answer.push_back(vector<int>{start[LeftPoint], finish[RightPoint]});
        }
        return Answer;        
    }    
};
```
