- Recursion vs DFS (search algorithm)

DFS, in more general scope, is one kind of search algorithm

DFS 的一种常见的实现implementation是 recursion



- Back-tracking vs dfs

Back-tracking describes the behavior of DFS



所有的permutation 和 combinition 都需要dfs解决

如果只需要打印个数，一般情况下可以用dp优化



## DFS 基本方法

1. How many levels in the recursion tree? what does it store on each level?
2. How many different states should we try to put on each level?

## DFS 四道母题

### 1. subset

凡是每个字符有两种可能性，加或者不加，要往subset 考虑

print all subsets of a set

**How many levels?**

The number of characters, each level represents one letter

**How many branches for each node?**

Two branch, one for add this letter, one for not add

```
													{}
									/                   \ 
							{a}											 {}
				   /       \               /           \
				 {a, b}    {a}						{b}          {}
			   /   \      /  \          /  \          / \
{a, b, c}  {a, b} {a, c} {a}    {b, c} {b}     {c} {}
```

append的数量和remove的数量 必须exactly same， 不一致一定错❌

⚠️ 写代码的时候 吃 和 🤮一定配对！！！吃了不吐撑死你

```java
void findSubset(char[] input, int level, StringBuilder sb) {
	if (index == input.length) {
		System.out.println(sb);
	}
  sb.append(input[level]); // 吃
	findSubset(input, level + 1, sb); 
  sb.deleteCharAt(sb.length() - 1); // 🤮 
  findSubset(input, level + 1, sb);	
}
```

homework：

1. Input = "abcde" add a space between two char, find all possible result
2. 



变种1: what if input = a b1 b2 b3 c

solution 1: each level consider 1 type of letters

solution 2: each level consider 1 letter



### 2. {} parenthesis

find all valid permutation using the parenthesis provided.

**How many levels?**

The number of parenthesis, each level represents one parenthesis

**How many branches for each node?**

Two branch, one for add left {, one for add right }



```java
public void findAllParenthesis(int n, int l, int r, StringBuilder sb) {
  if (l + r = 2 * n) {
    System.out.println(sb);
    return;
  }
  
  if (l < n) {
    sb.append('('); // 吃
    findAllParenthesis(n, l+1, r, sb);
    sb.deleteCharAt(sb.length() - 1); //🤮
  }
  
  if (l > r) {
    sb.append(')'); // 吃
    findAllParenthesis(n, l, r+1, sb);
    sb.deleteCharAt(sb.length() - 1); //🤮
  }
}
```



### 3. 99 cents / combination

```
                               99 cents
			        /			        | 						| 					\
L0(25c)  		25 * 0        25 * 1			25*2						 25*3

L1(10c)       

L2(5c)

L3(1c)

The recursion tree has 4 levels, each node has at most 99 branches
Time: O(99^4)
```



两种方法，用stringbuilder 或 fix size array



### 4. permutation

**How many levels?**

The number of chars, each level represents a position

**How many branches for each node?**

At most n and each level - 1



凡是permutation的问题首选 Swap swap



### Discussion

1. subset: 两种可能性，either or 类 首选subset
2. (): all kinds of {}
3. 99 cents: all kind of numbers problem +-*/
4. Permutation => whenever every single permutation contains all elements in the initial input, then you should consider swap swap





DFS vs BFS

- 正确性dfs可以
- space: need very large queen size, recursion tree grow exponentially.