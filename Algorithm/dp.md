Dp 的核心思想类似于我们高中的数学归纳法

1. 把一个大问题的解决办法用比他小的问题来解决，也就是思考从问题size = n - 1 增加到 size = n的时候
2. DP和recursion的关系
   1. recursion从大到小来解决问题，不记录任何sub-solution
      - base case
      - recursive rule
   2. dp 从小到大来解决问题，记录sub-solution
      - size 的subsolutions -> size n 的solution
      - base case
      - induction rule



### 1D dp

let me run a example

Ok, let's me explain the solution





一维的original data (such as a rope, a word), 求Max or Min (cut, merge)

Linear scan and look back to the previous elements

- Longest Ascending subarray (linear scan and look back i -1 element)

  M[i] represents the length of the longest ascending subarray inlcuding the i-th index

  index =  0  1  2  3  4  5  6 

  array  =  7  2  3  1   5  8  9

  dp	  =  1  1  2  1   2   3  4



​		Base case: dp[0] = 1

​		Induction rule: dp[i] = dp[i - 1] + 1		iff input[i] > input[i - 1]

​														1				 else



- longest ascending subsequence (linear scan and look back 0 ... i - 1)

  

  solution 1:

  dp[i] represents the longest subsequence from 0 to j including jth

  

  dp[i] = Max(dp[j] + 1)				if dp[j] < dp[i],   0 <= j < i

  otherwise, dp[i] = 1

  

  solution 2: 

  ```
  a = {7 , 2 ,3 ,1, 5, 8, 9, 6}
  
  bestAcdSequence[i]: represents the smallest the ending value of all ascending sebsequence with length i.
  idx   1	2	3	4	5	....
  best: 1 3 5 6 9 
  
  
  find the largest smaller index
  case 1: index == length => length++, best[length] = array[i];
  case 2: best[index + 1] = array[i];
  
  
  return best[length]
  
  
  b[0] = 0;
  t1: a[i] = 7, b[1] = 7; length = 1;
  t2: a[i] = 2, b[1] = 2; length = 1;
  t3: a[i] = 3, b[2] = 3; length = 2;
  ...
  
  
  time: O(n * log n)
  space: O(n)
  
  
  if we want to print the any longest subsequece
  we can use the array pred[i] to represent the index of predecessor of a[i]
  
  ```

  Follow up 1: print any longest ascending subsequence

  Follow up 2: print all  longest ascending subsequence

  

  

- Cut rope
  - Maximal Product when cutting rope

    ```java
    ___|___| ___| ___
    
    public int getMaxProduct(int n) {
    	if (n <= 1) {
    		return 0;
    	}
    }
    
    use dfs, time is O(2^n)
    
    
    
    dp solution 左大段 （可以查表格），右小段(再也不懂动的情况)
    
    1. base case: 
    dp[0] = invalid
    dp[1] = invalid
    
    
    2. induction rule
    
    dp[i] = max(k, dp[k]) * (i - k)   [k from 0 to i - 1]
      
    dp[2] = 1 (only one possible way to cut)
    
    Left part: 
    - two cases:
    	case 1 : cut at least one time (check table dp[j])
      case 2: no cut (just j)
    
    Right part: i - j
    
    dp[i] = Math.max(dp[i], left part * right part)    for each possible left part and right part
      
      
    public int cutRope(int n) {
    	int[] M = new int[n + 1]; // think about why n + 1?????? consider rope with 0 length
    	M[0] = 1;
    	M[1] = 0;
    	for (int i = 2; i <= n; i++) {
    		int curMax = 0;
    		for (int j = 1; j < i; j++) {
    			curMax = Math.max(curMax, Math.max(j, M[j]) * (i - j));
          																大段 = j 				小段 = i - j
    		}
    		M[i] = curMax;
    	}
    	return M[n];
    }
    
    ```

- cut dictionary (跟切绳子完全是一道题)

  Given a word, can it be composed by contatenating words from a given dictionary? 

  Dictionary: bob cat rob

  

- Cut palindrome

- jump game (1, 2, 3, 4变种)

  - 3 2 1 0 3

  ```java
  dp solution: O(n^2)
  
  
    
   
    
    
    
  Greedy solution: O(n)
  
  we can maintain a can_reach position, we care about how far we can reach and update it
  
  public boolean canJump(int[] numbers) {
    int canReach = 0;
    for (int i = 0; i <= canReach; ++i) {
      canReach = Math.max(canReach, i + array[i]);
      if (canReach >= array.length - 1) {
        return true;
      }
    }
    return false;
  }
  
  
  ```

  

### 2D dp

### 中心开花

* Cutting wood:

There is a wooden stick with length L >= 1, we need to cut it into pieces, where the cutting positions are defined in an int array A. The positions are guaranteed to be in ascending order in the range of [1, L - 1]. The cost of each cut is the length of the stick segment being cut. Determine the minimum total cost to cut the stick into the defined pieces.

**Examples**

- L = 10, A = {2, 4, 7}, the minimum total cost is 10 + 4 + 6 = 20 (cut at 4 first then cut at 2 and cut at 7)

处理时候的小tips

新建一个size 为 cuts.length + 2 的新array， 将0和length存在开头和结尾，这方便之后dp进行conner case的处理

```java
array[i]: represent the cut point i of the wood (including 0 and length)
dp[i][j]: represent the minimum cost to cut the stick between i and j
target result: dp[0][array.length - 1]

dp[i][j] = Min(dp[i][k] + dp[k][j] + array[j] - array[i])   i < k < j
```





99 cent 求多少种凑法



### maxtrix问题

2.1.1 连续最长1的问题

	- 火柴棍
	- X
	- +



**2.1.2 Matrix Largest Sum**

xxxxxxxx

xxxxxxxx

xxxxxxxx

xxxxxxxx

processing: vertical Prefix sum

do largest subarray sum



**2.1.3 Matrix Largest Area**

Given a matrix with 0 and 1. Find the rectangle with the largest area that consists of 1



- **Step1:** for botthom row = 0-th ... n-1 row, we calculate the continuous 1s height for each column => 1 D input array[1221133]

- **step2:** use 1D input array returned from step1, calculate the largest rectangle's area with the helper function.





2.1.4 国际象棋电话薄问题

```
dp[i][j]: represents the number of combination when we press i times ends with j

result: dp[0...k][n]

```



### Two strings 问题

这类问题只需要看小一号问题

S1的前i 个 letter 和 S2 的前j个letter

```
M[i][j] from M[i-1][j], M[i][j-1], M[i-1][j-1]
```



Minimum Edit Distance

Longest Common Substrings

Longest Common subsequence

widcard pattern substring

```
inlcude the characters ? *
? : match any single character
* : match 0 ... n characters
```



S1 input = XXXXXXXX

S2 parttern = YYYYYYY = ????

```java
Case1: Y = letter
		M[i][j] = true iff S1[i-1] == S2[j-1]
Case2: Y = ?
    M[i][j] = M[i-1][j-1]
Case3: Y = *
  	3.1 M[i][j] = M[i][j-1]
  	3.2 M[i][j] = M[i-1][j-1]
  	3.3 M[i][j] = M[i-2][j-1]
    ....
 	 	3.k M[i][j] = M[i-k][j-1]
  
  -------------------- Or -----------------------
  
    M[i][j] = M[i][j-1] // * match 0 letter
    						|| M[i-1][j] // * matches 1 or more letters
```



Case1: Y = letter