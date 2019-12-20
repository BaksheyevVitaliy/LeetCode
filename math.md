# Math

+ [Fibonacci Number Slow Recursion](#fibonacci-number-slow-recursion)
+ [Fibonacci Number Fast Recursion](#fibonacci-number-fast-recursion)
+ [Fibonacci Number Iteration](#fibonacci-number-iteration)
+ [Count Primes](#count-primes)

https://leetcode.com/problems/fibonacci-number/

## Fibonacci Number Slow Recursion

```C++
class Solution {
public:
    int fib(int N) {
        if(N <= 1)
          return N;
        else
            return fib(N - 1) + fib(N - 2);        
    }
};
```

## Fibonacci Number Fast Recursion

```C++
class Solution {
public:
    int fast(int N, int* arr){
        if(N <= 1)
          return N;
        if(arr[N] < 0)
          arr[N] = fast(N - 1, arr) + fast(N - 2, arr);
        return arr[N];
    }
    int fib(int N) {
        int *arr = new int[N + 1];
        for(int i = 2; i < N; i++){
            arr[i] = -1;
        }
        return fast(N, arr);
    }
};
```

## Fibonacci Number Iteration

```C++
class Solution {
public:
    int fib(int N) {
        int first = 0, last = 1, i = N;
        while(i--){
            last += first;
            first = last - first;
        }            
        return first;
    }
};
```

## Count Primes

https://leetcode.com/problems/count-primes/
```C++
class Solution {
public:
    int countPrimes(int n) {
        vector<int> Erastoph(n, 0);
        int ans = 0;
        for(int i = 2; i < n; i++){
            if(Erastoph[i] == 0){
                ans++;
                int j = 2;
                while(i * j < n){
                    Erastoph[i*j] = 1;
                    j++;
                }
            }
        }
        return ans;
        
    }
};
```
