从小养成一个好的学习习惯

知道什么是重要的，什么是该总结的，知道什么时候该做什么事

人想做成一件事就有一个理由（i c）

做不成一个事有无数成理由

```
1. Document your assumptions
2. Explain your approach and how you intend to solve the problem
3. Provide code comments where applicable
4. Explain the big-O run time complexity of your solution. Justify your answer.
5. Indentify any additional data structures you used and justify why you used them.
6. Only provide your best answer to each part of the question
```



------

## Class 2 recursiton I

Recursion的三个层次的理解：

- 表象上：
- 实质上：big problem to
- implementation: 
  - 1. base case： how to solve smalle problem
  - 2. recursive rule: how to make the pro



Recursion里面每一个node等于每一次function call

- 时间复杂度就是所有的node数量 * 每个node所需要的时间

冯诺伊曼计算机体系，任何时候都有唯一一个状态，这也就促成了call stack机制

- 空间复杂度：call stack直上直下的每个node消耗内存的加权



### Q1: Fibonacci number F(n) = F(n-1) + F(n-2) 

### Q2: Calculate a^b

```java
// Solution 1
// Time = O(n)
// Space = O(n)
public int calculateApowerB(int a, int b) {
	if (b == 0) {
    return 1;
  }
  return return a * calculateApowerB(a, b - 1);  
}

// Solution 2
// Time = O(n * log n)
// Space = O (n)
public int calculateApowerB(int a, int b) {
  if (b == 0) {
    return 1;
  }
  int temp = calculateApowerB(a, b/2);
  return b % 2 == 0 ? temp * temp : temp * temp * a;   }      
}
```



### Q3: Sorting algorithm

* election sort

每一轮筛选出来一个没有排好序的元素，并和没有排好序的最左端 swap一下。

In high level： consists of 2 for loops, for the outer loop, which means how many iterations I need t run. For the inner loop, I will find the global min from the rest elements. I swap the global min with the most left unsorted element.  

举一反二

How to use 3 stack to do the selection sort?



* Merge sort

  借助了recursion 的思想，把大的一个数组，拆成两个数组，如果两个数组都排好序了，通过谁小易谁合并两个数组。

-  Quick sort

  High level idea is use recursion to solve this problem. Each time, we randomly pick a pivot number, and we put all the elements smaller than pivot to its left, and all the elements greater or equal than pivot to its right. After this step, the pivot number is on its right position. And then we recursively use the same way to solve pivot's left part and pivot's right part until the whole array is sorted.

  Time: on average is O(n*l)





3 	1 	2	 4 	8 	7 	5 	6

​                  (pivot)



Worse case: n + n-1 + n-2 + ... + 1 = O(n^2)

Average case: O(nlogn)

两个挡板i, j 生成了三个区域

[0...i): 全部比pivot小的数

[i ... j ] : i和j之间为未知探索区域

(j... n-1]: 全部比pivot大或等于的数字



当i, j交错的时候（一定不是相遇）把pivot和i交换。因为此时维护了物理意义，j的右侧全是大于等于pivot的数



根据quicksort的思想，我们可以延伸到quick selection.

Q: find the smallest k elements in array?

```java
// Quickselct
// input:
// output:
public void quickSelect(int[] array, int k) {
  
  if (array == null || array.length <= k) {
    return array;
  }
  return quickSelect(array, k, 0, array.length - 1);
}

public void quickSelect(int[] array, int k, int left, int right {
  int pivot = partition(array, left, right);
  // left ... pivot ... right  1 2 3 4
//  														 l p   r
  if (pivot - left + 1 == k) {
    return;
  } else if (pivot - left + 1 > k) {
    quickSelect(array, k, left, pivot - 1);
  } else if (pivot -left + 1 < k) {
    quickSelect(array, k - (pivot - left + 1), pivot + 1, right);
  }
}

private int partition(int[] array, int left, int right) {
  int pivot = right;
  right--;
  while (left <= right) {
    if (array[left] < array[pivot]) {
      left++;
    } else if (array[right] >= array[pivot]) {
      right--;
    } else {
			swap(array, left++, right--);
    }
  }
  swap(array, left, pivot);
  return left;
}
                        
private void swap (int[] array, int left, int right) {
  int temp = array[left];
  array[left] = array[right];
  array[right] = temp;
}
```