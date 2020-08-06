HashTable:

- Find the common number between two sorted array?

拿到一道简单的题的时候一定不要着急propose a solution.

Clarification and assumption.

​			Sorted: ascending or descending

​			Duplicated number or not

​			how large of the two input array?

​			one array size is far large than the other? 

​			or same size in big o notation

Solution 取决于面试官告诉你的情景

1. use hashset

   - Time: O(n + m) in average, O(n*n + m*n) in worst case 

     (collision always happens)

   - Space: O(min(n, m))

2. use two pointer

   - Time: O(n + m)
   - space: O(1)

3. use binary search

   - Time: O(n * log m)  n << m (n = 10, m = 1M) 
   - Space: O(1)



## String

逻辑层面的数据结构，底层用char array 实现

Java: String, StringBuilder, StringBuffer

- StringBuilder vs StringBuffer
  - StringBuffer is *synchronized* i.e. thread safe. 
  - StringBuilder is *non-synchronized* i.e. not thread safe. (more efficient)

string技巧： 看前不看后！



### string常见的题型

1. Char removal

   1.1 remove some particular chars from a string

   1.2 remove all leading/trailing/duplicated empty spaces from a s tring.

2. De-duplication

   2.1 aaaaaabbbbccc -> abc

   2.2 aaabbbaaac -> c (俄罗斯方块)

3. Substring -> strstr （字串搜索）

   3.1 regular method

   3.2 rabin-carp (hash based string matching)

4. Reversal (swap) e.g. I love yahoo -> yahoo love I

   - reverse the words in string
   - e.g. shift the whole string to right-hand side by 2 position (rotate)
     - Step 1: reverse the whole string
     - Step2: reverse the first two, and reverse the last elements

5. replace some character with others

   clarification: 

   - the string has overlap or not. s1 = aa, aaa -> cfa 

   Case 1: replaced length >= substitude length

   Case 2: replaced length < substitude length



Advanced operations (Defer to string II)

- Move letters around e.g. ABCD 1234 -> A1B2C3D4
  - method 1: define a custom order, then sort the string
  - Method2: like a reverse version of merge sort
    - 当左右为基数的时候，要保证左右的取法一样 （AB CDE | 12 345)
    - 使用rotate方法可以避免conner case 处理
- Permutation (use DFS)
  - 没有duplicate
    - each level decide a character
    - Each node has n! 
  - 有 duplicate
    - use a hashset to record currently used, and avoid the same subtree

- decoding/ encoding aaaabcc -> a4b1c2

  - Encoding 比较容易
  - Decoding 相对复杂 （因为要考虑新的空间，无法in place）

- Longest substring that contains only unique chars

  - use a sliding window [i, j]  represents the longest substring ending with j

  - initial state: i = 0, j = 0

  - j++ until set.contains(array[j])

  - i++ until substring[i...j] does not contain any duplicate

    

- Smallest substring that contains all given chars

- Matching (*, ?)

- ...



string concat 一个字符 O(n), 但是用stirngbuilder append一个字符到末尾O(1)



