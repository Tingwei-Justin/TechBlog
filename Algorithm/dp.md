一维dp



二维dp



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