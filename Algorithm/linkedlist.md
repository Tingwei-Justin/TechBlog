# LinkedList

Key points when you solve the linkedlist：

1. when you want to dereference a ListNode, make sure it is not a NULL pointer

   e.g. p.next.next.value

2. Never ever lose the control of the head pointer of the linkedlist



When to use dummy head?

```
when we want to build a linkedlist from scratch. In order to avoid null pointer dereference, we need to use a dummy head.
```



Common question:

1. Reverse linkedlist (1, 2, 3, ... k)
2. Find the middle of linkedlist
3. Insert a node into linkedlist

### Question 1 Reverse linkedlist (Basic)

- Method 1: iterative way

Basically, i will use 3 variable to solve this problem. 

**prev:** the node and all the node before it have already reversed

**head:** current node which need to reverse

**next:** temporily save the new head to avoid lose the control of the head.



this func takes one arguments, it represents, the return type is ...



```java
public ListNode reverseLinkedList(ListNode head) {
	ListNode pre = null;
  while (head != null) {
    ListNode next = head.next;  // store the head of remaining linkedlist
    head.next = prev;   // reverse step
    prev = head;
    head = next;
  }
  return prev;
}
```





- Method 2: recursive way

n1 - >          | n2 -> n3 -> n4 -> null|

​                           subproblem



```java
public ListNode reverseLinkedList(ListNode head) {
	if (head == null || head.next == null) {  // base case
		return head;
	}
	
	ListNode newHead = reverseLinkedList(head.next);
	head.next.next = head;
	head.next = null;
	
	return newHead;
}
```



## Question 2 Reverse linkedlist with 2 nodes, 3 nodes, or k nodes

input: (N1 - > N2) -> (N3 - > N4) -> (N5 -> N6) -> NULL

Output: (N2 - > N1) -> (N4 - > N3) -> (N6 -> N5) -> NULL



```java
// recursion
public ListNode reverseLinkedListByPair(ListNode head) {
	// base case
	if (head == null || head.next == null) {
		return head;
	}
	ListNode nextHead = reverseLinkedListByPair(head.next.next);
	ListNode newHead = head.next;
	newHead.next = head; // reverse action
	head.next = nextHead;
	return newHead;
}

// iteration
// 1 ->  2 ->  3 -> 4
// n1    n2    n3
// h

public ListNode reverseLinkedListByPair(ListNode head) {
  if (head == null || head.next == null) {
    return head;
  }
  
  ListNode newHead = head.next;
  while (head != null && head.next != null) {
    ListNode nextHead = head.next.next;
    head.next.next = head; // reverse step;
    // connect with nextHead
    if (nextHead != null && nextHead.next != null) {
      head.next = nextHead.next;
    } else {
      head.next = nextHead;
    }
    head = nextHead;
  }
  return newHead;
}
```



input: (N1 - > N2 -> N3) - > (N4 -> N5 -> N6) -> NULL

​			 n1.     n3.      n3

Output: (N3 -> N2 - > N1) ->(N6 -> N5->N4) -> NULL

```java
public ListNode recursion(ListNode head) {
	if (head == null || head.next == null || head.next.next == null) {
		return head;
	}
	ListNode nextHead = recursion(head.next.next.next);
	ListNode n1 = head;
	ListNode n2 = n1.next;
	ListNode n3 = n2.next;
	n3.next = n2;
	n2.next = n1;
	n1.next = nextHead;
	return n3;
}
```



```java
// Time: O(n) including find k-1 nodes and reverse k nodes
// Space: O(n/k) call stack
public ListNode reverseKGroupRecursion(ListNode head, int k) {
    // base case
    ListNode newHead = getNext(head, k-1);  //return null if there is not enough k - 1 nodes
    if (newHead == null) {
      return head;
    }
    
    // recursive rule
    ListNode nextHead = reverseKGroupRecursion(tail.next, k);
    newHead.next = null;  // cut the linkedlist
    reverse(head); // reverse current k
    head.next = nextHead; // concat
    return newHead;
  }

/*
	Get next k nodes from head
	return null if there is not enough k nodes
*/
  private ListNode getNext(ListNode head, int k) {
    if (head == null) {
      return head;
    }
    for (int i = 0; i < k; i++) {
      if (head.next == null) {
        return null;
      }
      head = head.next;
    }
    return head;
  }
	
/*
	Reverse the linkedlist
*/
  private ListNode reverse(ListNode head) {
    if (head == null || head.next == null) {
      return head;
    }
    ListNode newHead = reverse(head.next);
    head.next.next = head;
    head.next = null;
    return newHead;
  }
```




## Question 3 Find the mid of the linkedlist

Find the middle node:

- first one in the mid two nodes

  1 -> 2 -> 3 -> 4 -> null.  => return 2

  **Keep fast in even node position**

  initilization: slow = head, fast = head.next

  termination condition: fast != null && fast.next != null

  

- second one in the mid two nodes

  1 -> 2 -> 3 -> 4 -> null.  => return 3

  **Keep fast in odd node position**

  initilization: slow = head, fast = head

  termination condition: fast != null && fast.next != null



Online algorithm  vs   Offline algorithm 

**Online algorithm:** use fast, slow pointer

**Offline algorithm:** traverse the linkedlist and count the number of nodes, and then traverse the count/2 number of nodes



check cycle ?

insert a node into a sorted linkedlist

insert a node into a cycle sorted linkedlist





## Question 4 

N1 -> N2 -> N3 -> N4 -> N5 -> N6 -> ... -> Nn -> null  (convert to)

(N1 -> Nn) -> (N2 -> Nn-1) -> ...

Step 1: find the mid

Step 2: reverse the second half

Step 3: merge





Method 2: use recursion to solve this problem

1 -> 2 -> 3 -> 4 

 c                

1 - > 4 -> 2 -> 3

​                c

1 -> 2 -> 3 -> 4 ->. 5

1 - > 5 - > 2 ->4 -> 3

```java


```

