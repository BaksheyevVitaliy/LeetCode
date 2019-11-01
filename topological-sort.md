# Topological Sort

+ [Course Schedule](#course-schedule)
+ [Course Schedule II](#course-schedule-ii)
+ [Verifying an Alien Dictionary](#verifying-an-alien-dictionary)


https://leetcode.com/problems/course-schedule/

## Course Schedule
```C++
bool Order(vector<vector<int>>& graf, int* color, int numberOfCourse){
    int j;
    if(color[numberOfCourse] == 2){
        return true;
    }
    if(color[numberOfCourse] == 1){
        return false;
    }
    color[numberOfCourse] = 1;
    for(j = 1; j < graf[numberOfCourse].size(); j++){
        if(Order(graf, color, graf[numberOfCourse][j]) == false)
                return false;
    }
    color[numberOfCourse] = 2;
    return true;
}

class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        int *color = new int[numCourses];
        vector<vector<int>> graf;
        int i = 0, j = 0;
        if (numCourses == 0)
            return true;
        for(i = 0; i < numCourses; i++){
            graf.push_back(vector<int>{i});
            color[i] = 0;
        }
        i = 0;
        while(i < prerequisites.size()){
            j = 1;
            while(j < prerequisites[i].size()){
                graf[prerequisites[i][0]].push_back(prerequisites[i][j]);
                j++;
            }
            i++;
        }
        for(i = 0; i < numCourses; i++){
            if(Order(graf, color, i) == false)
                return false;
        }
        return true;
        
    }
};
```
https://leetcode.com/problems/course-schedule-ii/

## Course Schedule II

```C++
bool Order(vector<vector<int>>& graf, int* color, vector<int>& ordering, int numberOfCourse){
    int j = 1;
    if(color[numberOfCourse] == 2){
        return true;
    }
    if(color[numberOfCourse] == 1){
        return false;
    }
    color[numberOfCourse] = 1;
    for(j = 1; j < graf[numberOfCourse].size(); j++){
        if(Order(graf, color, ordering, graf[numberOfCourse][j]) == false)
                return false;
    }
    ordering.push_back(numberOfCourse);
    color[numberOfCourse] = 2;
    return true;
    
}

class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        int *color = new int[numCourses];
        vector<int> ordering;
        vector<vector<int>> graf;
        int i = 0, j = 0;
        if (numCourses == 0){
            return {};
        }
        for(i = 0; i < numCourses; i++){
            graf.push_back(vector<int>{i});
            color[i] = 0;
        }
        i = 0;
        while(i < prerequisites.size()){
            j = 1;
            while(j < prerequisites[i].size()){
                graf[prerequisites[i][0]].push_back(prerequisites[i][j]);
                j++;
            }
            i++;
        }
        for(i = 0; i < numCourses; i++){
            if(Order(graf, color, ordering, i) == false){
                return {};
            }
        }
        return ordering;
        
    }
};
```

https://leetcode.com/problems/verifying-an-alien-dictionary/

## Verifying an Alien Dictionary

```C++
bool Compare(string word1, string word2, string order){
    int passOrder = 0, pass1 = 0, pass2 = 0;
    while((pass1 < word1.length())&&(pass2 < word2.length())){
        if(word1[pass1] == word2[pass2]){
            pass1++;
            pass2++;
        }
        else{
            for(passOrder = 0; passOrder < order.length(); passOrder++){
                if(order[passOrder] == word1[pass1])
                    return true;
                if(order[passOrder] == word2[pass2])
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
            if(!(Compare(words[i], words[i + 1], order)))
                return false;
        return true;
    }
};
```
