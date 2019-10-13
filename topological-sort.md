# Topological Sort

+ [Course Schedule](#course-schedule)
+ [Course Schedule II](#course-schedule-ii)
+ [Verifying an Alien Dictionary](#verifying-an-alien-dictionary)


https://leetcode.com/problems/course-schedule/

## Course Schedule
```C++
bool myfunction(vector<int>& a, vector<int>& b) {
    return (a[0] < b[0]);
}

bool Order(vector<vector<int>>& Graf, int* color, int NumberOfCourse){
    int j;
    if(color[NumberOfCourse] == 2){
        return true;
    }
    if(color[NumberOfCourse] == 1){
        return false;
    }
    color[NumberOfCourse] = 1;
    for(j = 1; j < Graf[NumberOfCourse].size(); j++){
        if(Order(Graf, color, Graf[NumberOfCourse][j]) == false)
                return false;
    }
    color[NumberOfCourse] = 2;
    return true;
}

class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        int *color = new int[numCourses];
        vector<vector<int>> Graf;
        int i = 0, j = 0;
        if (numCourses == 0)
            return true;
        for(i = 0; i < numCourses; i++){
            Graf.push_back(vector<int>{i});
            color[i] = 0;
        }
        i = 0;
        while(i < prerequisites.size()){
            j = 1;
            while(j < prerequisites[i].size()){
                Graf[prerequisites[i][0]].push_back(prerequisites[i][j]);
                j++;
            }
            i++;
        }
        for(i = 0; i < numCourses; i++){
            if(Order(Graf, color, i) == false)
                return false;
        }
        return true;
        
    }
};
```
https://leetcode.com/problems/course-schedule-ii/

## Course Schedule II

```C++
bool myfunction(vector<int>& a, vector<int>& b) {
    return (a[0] < b[0]);
}

bool Order(vector<vector<int>>& Graf, int* color, vector<int>& ordering, int NumberOfCourse){
    int j = 1;
    if(color[NumberOfCourse] == 2){
        return true;
    }
    if(color[NumberOfCourse] == 1){
        return false;
    }
    color[NumberOfCourse] = 1;
    for(j = 1; j < Graf[NumberOfCourse].size(); j++){
        if(Order(Graf, color, ordering, Graf[NumberOfCourse][j]) == false)
                return false;
    }
    ordering.push_back(NumberOfCourse);
    color[NumberOfCourse] = 2;
    return true;
    
}

class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        int *color = new int[numCourses];
        vector<int> ordering;
        vector<vector<int>> Graf;
        int i = 0, j = 0;
        if (numCourses == 0){
            vector<int> nothing;
            return nothing;
        }
        for(i = 0; i < numCourses; i++){
            Graf.push_back(vector<int>{i});
            color[i] = 0;
        }
        i = 0;
        while(i < prerequisites.size()){
            j = 1;
            while(j < prerequisites[i].size()){
                Graf[prerequisites[i][0]].push_back(prerequisites[i][j]);
                j++;
            }
            i++;
        }
        for(i = 0; i < numCourses; i++){
            if(Order(Graf, color, ordering, i) == false){
                vector<int> nothing;
                return nothing;
            }
        }
        return ordering;
        
    }
};
```

https://leetcode.com/problems/verifying-an-alien-dictionary/

## Verifying an Alien Dictionary

```C++
bool Compaire(string word1, string word2, string order){
    int passorder = 0, pass1 = 0, pass2 = 0;
    while((pass1 < word1.length())&&(pass2 < word2.length())){
        if(word1[pass1] == word2[pass2]){
            pass1++;
            pass2++;
        }
        else{
            for(passorder = 0; passorder < order.length(); passorder++){
                if(order[passorder] == word1[pass1])
                    return true;
                if(order[passorder] == word2[pass2])
                    return false;
            }            
        }
    }
    if((pass1 < word1.length())&&(pass2 == word2.length()))
        return false;
    return true;
}
class Solution {
public:
    bool isAlienSorted(vector<string>& words, string order) {
        int i;
        for(i = 0; i < words.size()-1; i++)
            if(!(Compaire(words[i], words[i + 1], order)))
                return false;
        return true;
    }
};
```
