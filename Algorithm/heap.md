## Heap 知识点

- Heap property 堆的性质：

1. Complete binary tree （structure)
2. For every node, its value smaller / larger than its subchildren 堆序性 (order)



- Implemented as an unsorted array

1. index of lChildren = 2 * i + 1
2. index of rChildren = 2 * i + 2
3. index of parent = (i - 1) / 2



- Operations
  1. Insert: O(log n) - percolate up
  2. Pop: O(log n) - percolate down
  3. get/top : O(1)
  4. Update: O(log n)
  5. Heapify: O(n)



## Find the smallest k elements in unsorted array

**Solution 1: Use MaxHeap**

xxxxxx  xxxxxxxxx

​              i ->

Step 1: initially, we insert the first k elements into a Max-heap. Time: O(k)

Step 2: when a new element input[i] comes in, we compare input[i] with maxHeap.top()

​	case2.1 if input[i] < maxHeap.top(), we call maxHeap.pop() and then insert new to maxHeap

​	case2.2 else do nothing

​	time = (n - k) log (k)

   

**Solution 2: Use Minheap**

add all the elements to minheap,

minHeap.pop() n times

Time: O(n) + O(k * log n)

**Compare time of two solutions**

​							Max Heap (online algorithm)  					Min heap(offline algorithm)

​							(n - k) log (k)               									O(n) + O(k * log n)

k <<<n                nlogk																O(c * n)                								  hard to say

k ~~~~~~~n                n log n																n log n                 								hard to say





**Solution 3: Quick Select**

quicksort idea + binary search

我们可以想象每次归位的pivot作为binary search的mid

我们的目标是pivot == k

Time:

Avg: n + n/2 + n/4 +... + 1 = O(n)

Worst case: O(n^2)





Java PriorityQueue

- implement Queue interface

如何实现prority heap

- Method 1: Comparable

```
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
```

```
interface Comparable<E> {
	int compareTo(E ele);
}
```

```java
class Integer implements Comparable<Integer> {
	@Override
	public int CompareTo(Integer another) {
		if (this.value == another.value) {
			return 0;
		}
		return this.value < another.value ? -1 : 1;
	}
}
```



Method 2: Comparator

provide an extra comparator object to compare the elements



```java
interface Comparator <E> {
	int compare(E o1, E o2);
}


class MyComparator implements Comparator<Integer> {
	@Override
	public int compare(Integer i1, Integer i2) {
		if (i1.equal(i2)) {
			return 0;
		}
		return i1 < i2 ? 1 : -1;
	}
}
```

```
// 如果想实现object.compareTo的相反顺序
Collections.reverseOrder()
```





数组 vs treenode 来实现一个tree

high level idea is a tree structure, but in detail we use array to implement a tree



1. 输入输出都是array, 中间不需要其他数据结构的转换
2. overhead小，random access, locality





Implement a priority queue

Offer(): percolate up 

- Time: O(log n )  because complete tree, the height of complete tree is log n

poll(): percolate down

```java 
public class Heap {
	
  public int poll() {
    
  }
  
  public void offer() {
    
  }
  
  public void heapify() {
    for (int i = size / 2 - 1; i >= 0; i--) {
      percolateDown(i);
    }
  }
  
	private void percolateUp(int index) {
		while (index > 0) {
      int parentIndex = (index - 1) / 2;
      if (array[index] < array[parentIndex]) {
        swap(array, index, parentIndex);
        index = parentIndex;
      } else {
        break;
      }
    }
	}
	
	private void percolateDown(int index) {
		while (index <= size / 2 - 1) {
      // 一定有left 但是不一定有right
      int leftChildIndex = index * 2 + 1;
      int rightChildIndex = index * 2 + 2;
      int swapCandidate = leftChildIndex;
      if (rightChildIndex; <= size - 1 && array[rightChildIndex] < array[leftChildIndex]) {
        swapCandidate = rightChildIndex;
      }
			if (array[index] > array[swapCandidate]) {
        swap(arary, index, swapCandidate);
        index = swapCandidate;
      } else {
        break;
      }
    }
	}
}
```



Use PriorityQueue solve shortest path problem

Q1:  

input:

a[]: int sorted array

b[]: int sorted array

output: k-th smallest or all top k small elements

a: [2, 3, 5, 10, 15]

b:[3, 6, 9, 12]

```
My idea is to construct a 2d matrix, matrix[i][j] represents the a[i] + b[j].
According to a and b are sorted, so matrix[i][j] have two important properties
1. each row are sorted
2. each column are sorted

e.g.

[[5, 8, 11, 13],
 [6, 9, 12, 15],
 [8, 11, 14, 17],
 [13, 16, 19, 22],
 [18, 21, 24, 27]]
 
 Actually we don't really need to construct the real 2d matrix, we can have this sence in our mind.
 
 We can see for each element matrix[i][j], it must smaller than matrix[i+1][j] and matrix[i][j+1].
 
 matrix[i][j]  <= matrix[i][j+1]
 
 matrix[i][j]  <= matrix[i+1][j]
 
 Solution: we can use a minheap to solve this problem. 
 
 
 Solution 1:
 Initial state: minHeap.offer(matrix[0][0])
 
 For 1...k
 		we call minHeap.poll()
 		generate its two neighbours (right and bottom), add them to minheap
 
 Time: O(k * log k)
 space: O(k)
 Drawback: we need an additional set to deduplicate, because each state can be generate more than 1 times
 
 
 Solution 2:
 Initial state: minHeap.offer(matrix[0][0..n] or matrix[0..m][0])
 For 1...k
 		we call minHeap.poll()
 		generate its right or bottom neighbour, add to minheap
 
 Time: O(min(m,n) + k * log(k + min(m, n))  heapify + add and delete k times in heap
 Space: O(k + min(m, n)) use for heap
 
 
 Conclusion:
 
 If k <<<<<< min(m,n), prefer solution 1 
 If k ~== min(m,n), prefer solution 2
 If k >>>>> min(m,n) prefer solution 2
```



