# Queue & Stack

## Highlight

### 1. Queue

- Definition: FIFO == First in first out

- Common usages:

  - Breadth-First Search related problems
  - Sliding window

- Common questions:

  - Tree printout by level (level order traversal)

  - Sliding window problems (Deque: double ends manipulation)

    xxxx

    __

### 2. Stack

- Definition: LIFO == Last in first out, like a box
- Operations: push(), pop(), top()



### 3. Popular interview question related queue and stack

**Question 1: How to sort numbers with three stacks**

Follow up: How to sort numbers with two stacks

Idea: like selection sort idea, 





**Question 2: How could we implement a queue by using two stacks?**

Idea:

```
stack1 for push()
stack2 for pop(), if stack2 is empty, move all the element from stack1 to stack2, and then stack2.pop()

 Time complexity:

- Enqueue(): O(1)
- Dequeue(): worst case O(n), Amortized: O(1)
```





Follow up 1: How could we implement a stack by using two queues without know the size of queue

idea: 

```
stack: [1,  2, 3

Queue 1    <- 1 2 3 <-

Queue 2   <-     <-

push(): 
	- queue1.enqueue()
pop():
	- move all but the last element from q1 to q2
	- dequeue the last element from q1
	- swap the reference of q1 and q1
```



Follow up 2: How could we implement a stack by using one queues knowing the size of queue at any time

Idea:

```:
stack: [1,  2, 3

Queue     <- 1 2 3  <-

push():
 - q.enqueue()
 
pop():
- get size: q.size()
- do (size - 1) times
			x = q.dequeue()
			q.enqueue(x)
- q.dequeue()
```



**Question 3: How to implement the min() function when using stack with time O(1) for each operation?**

Idea:

```
using two stack

stack: nornal stack
minStack: track the min value of the stack

minstack : <value, index> to optimize the space
we only need to record the first minimum value so far is enough
```





**Question 4: How to use multiple stacks to implement a deque? (two or three stacks)**

idea:

```
         Left XxxxxxxxxxxxX Right
4 API
Left.add()                 Right.add()
Left.remove()							 Right.remove()

# Native solution
  use two stacks
        xxxxx] [xxxxx
        L           R

  add() 
    - is easy just add to left or right
    - time: O(1)

  remove()
   - stack is not empty, this case time is O(1)
   - stack is empty, we need to move all elements from one to another stack, and then pop()
     In this case, time is O(n)

# Optimize solution

	idea: if L and R each time have the roughly same numbers of element, the amortized time can be O(1)
				so we use another stack as buffer, to ensure each time we L and R have almost same numbers of elements 
  
  use three stacks
        xxxxx] [xxxxx
        L           R
        
        buffer: [

  add() 
    - is easy just add to left or right
    - time: O(1)

  remove()
   - stack is not empty, this case time is O(1)
   - stack is empty
     1. we move half elements from stack2 to buffer
     2. we move the remaining half elements from stack2 to stack1
     3. we move all the elements in buffer to stack2
     
     amortized time: O(1)
```

