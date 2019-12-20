
# String

+ [Longest Substring Without Repeating Characters](#longest-substring-without-repeating-characters)
+ [Longest Repeating Character Replacement](#longest-repeating-character-replacement)
+ [Minimum Window Substring](#minimum-window-substring)
+ [Group Anagrams](#group-anagrams)
+ [Valid Parentheses](#valid-parentheses)
+ [Generate Parentheses](#generate-parentheses)
+ [Valid Palindrome](#valid-palindrome)
+ [Longest Palindromic Substring](#longest-palindromic-substring)
+ [Palindromic Substrings](#palindromic-substrings)
+ [Is Subsequence](#is-subsequence)

## Longest Substring Without Repeating Characters

https://leetcode.com/problems/longest-substring-without-repeating-characters/
```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int startstring = 0;
        int finishstring = 0;
        int maximum = 0;
        for(finishstring = 0; finishstring < s.length(); finishstring++){
            for(int i = startstring; i < finishstring; i++){
                if(s[i] == s[finishstring])
                    startstring = i + 1;
            }
            maximum = max(maximum, finishstring - startstring + 1);
        }
        return maximum;
    }
};
```

## Longest Repeating Character Replacement

https://leetcode.com/problems/longest-repeating-character-replacement/
```C++
class Solution {
 public:
  int characterReplacement(string s, int k) {
    int maxCount = 0;
    int left = 0;
    int count['Z' - 'A' + 1] = {0};
    int answer = 0;
    for (int right = 0; right < s.size(); right++) {
      int windowSize = right - left + 1;
      maxCount = max(maxCount, ++count[s[right] - 'A']);
      if (windowSize - maxCount > k) {
        count[s[left++] - 'A']--;
      } else {
        answer = max(answer, windowSize);
      }
    }
    return answer;
  }
};
```

## Minimum Window Substring

https://leetcode.com/problems/minimum-window-substring/
```C++
class Solution {
public:
    string minWindow(string s, string t) 
{
	if (t.empty ())
		return "";
	unordered_map <char, vector <int>> char_cnt;
	for (auto &c : t)
	{
		if (char_cnt.count (c) == 0)
			char_cnt [c] = {0, 1};
		else
			char_cnt [c][1]++;
	}
	int left, right, ret_left = 0, ret_right = INT_MAX, found_cnt = 0;
	for (left = 0, right = 0; right < s.length (); right++)
	{
		if (char_cnt.count (s[right]) == 0)
			continue;
		char_cnt [s[right]][0]++;
		if (char_cnt [s[right]][0] <= char_cnt [s[right]][1])
			found_cnt++;
		while (left < right)
		{
			if (char_cnt.count (s[left]) == 0)                
			{
				left++;
				continue;
			}
			if (char_cnt [s[left]][0] > char_cnt [s[left]][1])
			{
				char_cnt [s[left]][0]--;
				left++;
				continue;
			}
			break;
		}
		if (found_cnt == t.length () && (right - left) < (ret_right - ret_left))
		{
			ret_left = left;
			ret_right = right;
		}
	}
	return found_cnt == t.length () ? s.substr (ret_left, ret_right - ret_left + 1) : "";
}
};
```

## Group Anagrams

https://leetcode.com/problems/group-anagrams/
```C++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<int> ar(26, 0);
        vector<vector<string>> ans;
        map <vector<int>, int> Used;
        int j = 0;
        for(int i = 0; i < strs.size(); i++){
            for(j = 0; j < strs[i].size(); j++){
                ar[strs[i][j] - 'a']++;
            }
            if(Used.find(ar) != Used.end()){
                ans[Used[ar]].push_back(strs[i]);
            }
            else{
                Used[ar] = ans.size();
                ans.push_back(vector<string>{strs[i]});
            }     
            for(j = 0; j < ar.size(); j++){
                ar[j] = 0;
            }
        }
        return ans;
    }
};
```

## Valid Parentheses

https://leetcode.com/problems/valid-parentheses/
```C++
class Solution {
public:
    bool isValid(string s) {
        stack <char> steck;
        for(int i = 0; i < s.length(); i++){
            if(s[i] == '(' || s[i] == '[' || s[i] == '{'){
                steck.push(s[i]);
            }
            else{
                if(steck.empty())
                    return false;
                if(s[i] == ')' && steck.top() != '('){
                    return false;
                }
                if(s[i] == ']' && steck.top() != '['){
                    return false;
                }
                if(s[i] == '}' && steck.top() != '{'){
                    return false;
                }
                    steck.pop();
                }
            }
        if(steck.empty())
            return true;
        return false;
    }
};
```

## Generate Parentheses

https://leetcode.com/problems/generate-parentheses/
```C++
class Solution {
    void Create(vector<string>& ans, string current, int n, int numberOfOpenBacket, int numberOfBackBacket){
        if(n == 0){
            ans.push_back(current);
            return;
        }
        if(numberOfOpenBacket - numberOfBackBacket == n){
            Create(ans, current + ')', n - 1, numberOfOpenBacket, numberOfBackBacket + 1);
            return;
        }
        if(numberOfOpenBacket == numberOfBackBacket){
            Create(ans, current + '(', n - 1, numberOfOpenBacket + 1, numberOfBackBacket);
            return;
        }
        Create(ans, current + '(', n - 1, numberOfOpenBacket + 1, numberOfBackBacket);
        Create(ans, current + ')', n - 1, numberOfOpenBacket, numberOfBackBacket + 1);
    }
public:
    vector<string> generateParenthesis(int n) {
        vector<string> ans;
        string current;
        Create(ans, current, n * 2, 0, 0);
        return ans;
    }
};
```

## Valid Palindrome

https://leetcode.com/problems/valid-palindrome/
```C++
class Solution {
public:
     bool isPalindrome(string s) {       
        for (int i = 0, j = s.size() - 1; j - i > 0; i++, j--)
        {
            while(i < s.size() && !isalnum(s[i])) i++;
            while(j >= 0 && !isalnum(s[j])) j--;
            
            if (j - i <= 0) return true;
            
            if (tolower(s[i]) != tolower(s[j])) return false;
        }
        
        return true;
    }
};
```

## Longest Palindromic Substring

https://leetcode.com/problems/longest-palindromic-substring/
```C++
class Solution {
public:
    string longestPalindrome(string s) {
        int maximum = 0;
        int maxStart = 0;
        int j = 0;
        if(s.empty())
            return s;
        for(int i = 0; i < s.length(); i++){
            j = 1;
            while((i + j < s.length())&&(i - j >= 0)&&(s[j + i] == s[i - j]))
                j++;
            if(maximum < (j - 1) * 2 + 1){
                maximum = (j - 1) * 2 + 1;
                maxStart = i - j + 1;
            }
        }
        for(int i = 0; i < s.length() - 1; i++){
            j = 0;
            while((i + j + 1 < s.length())&&(i - j >= 0)&&(s[j + i + 1] == s[i - j]))
                j++;
            if(maximum < j * 2){
                maximum = j * 2;
                maxStart = i - j + 1;
            }
        }
        return s.substr(maxStart, maximum);
    }
};
```

## Palindromic Substrings

https://leetcode.com/problems/palindromic-substrings/

```C++
class Solution {
public:
    int countSubstrings(string s) {
        int count = 0;
        int j = 0;
        int len = s.length();
        for(int i = 0; i < len; i++){
            j = 1;
            while((i + j < len)&&(i - j >= 0)&&(s[j + i] == s[i - j]))
                j++;
            count += j;
        }
        for(int i = 0; i < len - 1; i++){
            j = 0;
            while((i + j + 1 < len)&&(i - j >= 0)&&(s[j + i + 1] == s[i - j]))
                j++;
            count += j;
        }
        return count;
    }
};
```

## Is Subsequence

https://leetcode.com/problems/is-subsequence/
```C++
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int i = 0;
        int j = 0;

        while(j < s.length()){
            while(i < t.length() && t[i] != s[j])
                i++;
            if(i == t.length())
                return false;
            j++;
            i++;
        }
        return true;
            
    }
};
```
