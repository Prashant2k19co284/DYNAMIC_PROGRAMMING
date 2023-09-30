# BASIC CONCEPT OF DYNAMIC PROGRAMMING 

There are two point to use dynamic programming in recursive questions 
1) overlapping sub-problems 
2) only used for recurssive approach 
3) it reduces the time complexity of the code but space complexity may be vary

# FABONACCI QUESTION 

# NOTE*** with the itterative solution the recursion stacks does not implemented so reduces the stack flow or satck overflow 


```python
#using simple recursive approach 
#TIME COMPLEXITY =O(2**N) AND SPACE COMPLEXITY(O(N))
def fab_1(n):
    if n==0 or n==1:
        return n
    smalloutput_1=fab_1(n-1)
    smalloutput_2=fab_1(n-2)
    output=smalloutput_1+smalloutput_2
    return output
```


```python
# USING DYNAMIC APPROACH
# METHOD 1
#TIME COMPLEXITY = O(N) AND SPACE COMPLEXITY = (O(N))
def fab_dp(n,dp):
    if n==0 or n==1:
        return n
    if dp[n-1]==-1:
        smalloutput_1=fab_dp(n-1,dp)
        dp[n-1]=smalloutput_1
    else:
        smalloutput_1=dp[n-1]
    if dp[n-2]==-1:
        smalloutput_2=fab_dp(n-2,dp)
        dp[n-2]=smalloutput_2
    else:
        smalloutput_2=dp[n-2]
    output=smalloutput_1+smalloutput_2
    return output
```


```python
#METHOD 2
#TIME COMPLEXITY = O(N) AND SPACE COMPLEXITY = (O(N))
def fab_dp_2(n,dp_1):
    if n==0 or n==1:
        return n
    if dp_1[n]!=-1:
        return dp_1[n]
    else:
        dp_1[n]=fab_dp_2(n-1,dp_1)+fab_dp_2(n-2,dp_1)
        return dp_1[n]
```


```python
#RECURSION TO ITTERATIVE USING DP
#TIME COMPLEXITY = O(N) AND SPACE COMPLEXITY = (O(N))
def fab_dp_IT(n):
    dp[0]=0
    dp[1]=1
    for i in range(2,n+1):
        dp[i]=dp[i-1]+dp[i-2]
    return dp[n]
```


```python
# DIFFERENT SOLUTION 
#TIME COMPLEXITY = O(N) AND SPACE COMPLEXITY = (O(1))
def fab_IT_SP(n):
    a=0
    b=1
    for i in range(n):
        c=a+b
        a=b
        b=c
    return c
```


```python
n=int(input())
dp=[-1]*(n+1)
dp_1=[-1]*(n+1)
print(fab_IT_SP(n))
print(fab_dp_IT(n))
print(fab_dp_2(n,dp_1))
print(fab_dp(n,dp))
print(fab_1(n))

```

    5
    8
    5
    5
    5
    5
    

# COUNT WAYS TO REACH  N

QUS) You have been given a number of stairs. Initially, you are at the 0th stair, and you need to reach the Nth stair. Each time you can either climb one step or two steps. You are supposed to return the number of distinct ways in which you can climb from the 0th step to Nth step?



```python
#METHOD 1 RECCURSIVE ONLY
# n is always gretor than 0 if n is 0 then there is no base case 
def count_ways(n):
    if n==1 or n==2 :
        return n
    smalloutput_1=count_ways(n-1)
    smalloutput_2=count_ways(n-2)
    return smalloutput_1+smalloutput_2
```


```python
#METHODO 2 RECURSIVE APPROACH USING DP 
def count_ways_dp_rec(n,dp):
    if n==1 or n==2:
        return n
    if dp[n-1]==-1:
        smalloutput_1=count_ways_dp_rec(n-1,dp)
        dp[n-1]=smalloutput_1
    else:
        smalloutput_1=dp[n-1]
    if dp[n-2]==-1:
        smalloutput_2=count_ways_dp_rec(n-2,dp)
        dp[n-2]=smalloutput_2
    else:
        smalloutput_2=dp[n-2]
    return smalloutput_1+smalloutput_2

```


```python
#METHOD 3 DYNAMIC APPROACH USING ITTERATIVE METHOD 
def count_ways_dp_itr(n):
    dp=[-1]*(n+1)
    dp[1]=1
    dp[2]=2
    for i in range(3,n+1):
        dp[i]=dp[i-1]+dp[i-2]
    return dp[n]
```


```python
n=int(input())
dp=[-1]*(n+1)
print(count_ways_dp_itr(n))
print(count_ways(n))
print(count_ways_dp_rec(n,dp))
```

    5
    8
    8
    8
    

# FROG JUMP QUESTION

QUS) There is a frog on the '1st' step of an 'N' stairs long staircase. The frog wants to reach the 'Nth' stair. 'HEIGHT[i]' is the height of the '(i+1)th' stair.If Frog jumps from 'ith' to 'jth' stair, the energy lost in the jump is given by absolute value of ( HEIGHT[i-1] - HEIGHT[j-1] ). If the Frog is on 'ith' staircase, he can jump either to '(i+1)th' stair or to '(i+2)th' stair. Your task is to find the minimum total energy used by the frog to reach from '1st' stair to 'Nth' stair ?


```python
#METHOD 1 ONLY RECURSIVE APPROACH 
#TC=O(2**N) , SC=O(N)
#NOTE**(if the frog is at first step or n==1 then the total loss to reach the 0 will be the energy equivalent to the energy at height 1 stairs
#if the frog is at secong stair or n==2 then the minimum energy will be to reach the 0 stairs is second from 0 or second to first ) )
def frog_jump_rec(n):
    if n==1:
        return abs(height[n])
    if n==2:
        return min(abs(height[n]-height[n-2]),abs(height[n]-height[n-1]))
    return min((frog_jump_rec(n-1)+abs(height[n]-height[n-1])),frog_jump_rec(n-2)+abs(height[n]-height[n-2]))
```


```python
# Method 2 to use the dynamic programming with recursion 
#TC=O(N) AND SC=O(N)
def frog_jump_dp_rec(n,dp):
    if n==1:
        return abs(height[n])
    if n==2:
        return min(abs(height[n]-height[n-1]),abs(height[n]-height[n-2]))
    if dp[n-1]==-1:
        ans1=abs(height[n]-height[n-1])
        dp[n-1]=ans1
    else:
        ans1=dp[n-1]
    if dp[n-2]==-1:
        ans2=abs(height[n]-height[n-2])
        dp[n-2]=ans2
    else:
        ans2=dp[n-2]
    return min((frog_jump_rec(n-1,dp)+ans1),frog_jump_rec(n-2,dp)+ans2)
```


```python
# Method 3 to use the dynamic programming with recursion 
#TC=O(N) AND SC=O(N)
def frog_jump_dp_rec_2(n,dp):
    if n==1:
        return abs(height[n])
    if n==2:
        return min(abs(height[n]-height[n-1]),abs(height[n]-height[n-2]))
    if dp[n-1]==-1:
        ans1=frog_jump_dp_rec_2(n-1,dp)+abs(height[n]-height[n-1])
        dp[n-1]=ans1
    else:
        ans1=dp[n-1]+abs(height[n]-height[n-1])
    if dp[n-2]==-1:
        ans2=frog_jump_dp_rec_2(n-2,dp)+abs(height[n]-height[n-2])
        dp[n-2]=ans2
    else:
        ans2=dp[n-2]+abs(height[n]-height[n-2])
    return min(ans1,ans2)
```


```python
#METHOD 4 USING DP WITH ITTERATIVE METHOD 
#TC=O(N) AND SC=O(N) 
def frog_jump_dp_itr(n):
    dp=[-1]*(n+1)
    dp[0]=0
    dp[1]=abs(height[1])
    dp[2]=min(abs(height[2]-height[1]),abs(height[2]-height[0]))
    for i in range(3,n+1):
        ans1=dp[i-1]+abs(height[i-1]-height[i-1])
        ans2=adp[i-2]+abs(height[i-1]-height[i-2])
        dp[i]=min(ans1,ans2)
    return dp[n]
```

# Maximum sum of non-adjacent elements

QUS) You are given an array/list of ‘N’ integers. You are supposed to return the maximum sum of the subsequence with the constraint that no two elements are adjacent in the given array/list.


```python
#METHOD 1 USING RECURSION APPROACH ONLY 
def adjacent_max_sum(arr):
    if len(arr)==0:
        return 0
    smalloutput_1=arr[0]+adjacent_max_sum(arr[2:])
    smalloutput_2=adjacent_max_sum(arr[1:])
    return max(smalloutput_1,smalloutput_2)
    
```


```python
#METHOD 2 USING RECURSIVE APPROACH WITH DP
def adjacent_max_sum(arr,dp):
    if len(arr)==0:
        return 0 
```


```python
arr=[int(ele) for ele in input().split()]
adjacent_max_sum(arr)
```

    1 2 3 12 3 5 8 1 9
    




    31




```python

```
