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

