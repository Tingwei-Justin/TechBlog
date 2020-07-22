实现stack的时候只需要在linkedlist实现，在头上进行pop()和push(). 时间复杂度都是O(1)

如果在尾部的话，pop()在单链表的情况下无法做到O(1)操作

```java
Class ListNode {
  E value;
  ListNode next;
  public ListNode(E value) {
    this.value = value;
  }
}

Class Stack {
  private ListNode head;
 	private int size;
  
  public Stack() {
    size = 0;
  }
  
  public boolean push(E value) {
    ListNode node = new ListNode(value);
    node.next = head;
    head = node;
  }
  
  public E pop() {
    if (head == null) {
      return head;
    }
    ListNode prev = head;
    head = head.next;
    prev.next = null;
    return prev.value;
  }
}




```

用linked list 实现一个queue, 头出尾入

```java
public Class Queue {
	private ListNode head;
	private ListNode tail;
	
	public void offer(E element) {
    if (head == null) {
      head = new ListNode(element);
      tail = head;
    } else {
      tail.next = new ListNode(element);
    	tail = tail.next;
    }
	}
	
	public E poll() {
		if (head == null) {
    	return null;
    }
    ListNode prev = head;
    head = head.next;
    if (head == null) {
    	tail = null;
    }
    prev.next = null;
    return prev.value;
	}
	
	public E peek() {
		return head == null ? null : head.value;
	}
}
```

