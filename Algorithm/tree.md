在之前的学习中物理层面的数据结构只有array和linkedlist

stack, queue是逻辑层面的数据结构

碰到树可以跟面试官clarify一下是否有parent节点

```
class TreeNode {
	int value;
	TreeNode left;
	TreeNode right;
}
```

### 基本知识点1: Tree traversal

Tip: 一般来说把null作为base case触底反弹，而不是leaf node

Stack 在linux 上8Mb左右，在Mac,win上1Mb左右

少用recursion, 避免stackoverflow

使用recursion的时候分析一下数据量

- Pre-order: 先访问自己，再访问左子树，再访问右子树

  ```java
  // implementation with recursion
       3
     /   \
    2     4
   /  \
  1    4  
  
  public void preOrder (TreeNode root) {
  	if（root == null)
      return;
    System.out.println(root.value);
    preOrder(root.left);
    preOrder(root.right);
  }
  
  // implementation with iteration
  // method1: push left
  // method2: add right, add left
  需要回溯的是root.right
  
  模拟一个stack[]
  stack的特征是先进后出
  1. pop（）的时候先打印
  2. add right （因为想先打印left, 所以要先add right, 再add left
  3. add left
  
  public void preOrder (TreeNode root) {
    if (root == null) {
      return;
    }
    Deque<TreeNode> stack = new ArrayDeque<>();
    stack.offerFirst(root);
    while (!stack.isEmpty()) {
      TreeNode cur = stack.pollFirst();
      System.out.println(cur.key);
      if (cur.right != null) {
        stack.offerFirst(cur.right);
      }
      if (cur.left != null) {
        stack.offerFirst(cur.left);
      }  
    }
  }
  
  ```

  

- In-order：先访问左子树，自己，右子树

  ```java
  需要回溯的node 是root
       3
     /   \
    2     4
   /  \
  1    4  
  
  stack:[]
  从左子树回溯的时候打印自己
  
  method1: 
  1. 一路向左，将所有的遇到的node都push到stack里，until left == null
  2. cur = stack.pop(),  print(cur)
  3. addAllLeft(cur.right)
  
  method2: 
  next = store the next node which need to iterate
  
  case1: next = null, which means the leftsubtree has nothing, we can print the root of the top element in the stack.
  case2: next != null, continue go left and push the root to stack
  
  termination condition: next == null && stack.isEmpty()
  (当走到root节点的时候stack为空，但是helper不为空，所以这不是终止条件，我们只有在stack和helper都为空的时候才可以终止)
  
    
    /**
    	method1: push all the left node into stack
    */
  public void inorder(TreeNode root) {
    if (root == null) {
      return;
    }
    
    Deque<TreeNode> stack = new ArrayDeque<>();
    pushAllLeft(root, stack);
    while (!stack.isEmpty()) {
      TreeNode cur = stack.pollFirst();
      System.out.println(cur.key);
      pushAllLeft(cur.right, stack);
    }
  }
  
  private void pushAllLeft(TreeNode root, Deue<TreeNode> stack) {
    if (root == null) {
      return;
    }
    while (root != null) {
      stack.offerFirst(root);
      root = root.left;
    }
  }
  
  
  
  /**
  	method2: use helper variable to store next node which will explore
  **/
  
  public void inorder(TreeNode root) {
  	if (root == null) {
      return;
    }
    
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode next = root;
    
    while (!stack.isEmpty() || next != null) {
      if (next == null) {
        TreeNode cur = stack.pollFirst();  // 可以直接让 helper = stack.pollFirst()
        System.out.println(cur.key);
        next = cur.right;
      } else {
        stack.offerFirst(next);
        next = next.left;
      }
    }
  }
  
  
  
  ```

  

- Post-order：先访问左子树，右子树，自己

  ```java
  method1:
  
  left right root -> reverse -> root right left
  
  use two stack
  offline algorithm
  
  
  method2: 三顾茅庐
  idea: 第三次看到node的时候打印
  First: From top to bottom
  Second: From left child to parent
  Third: From right child to parent
    
    
  用current 和 pre来判断第几次遇见
   
          2
        /   \	
        1    3
  case1: pre == null || current == pre.left || current == pre.right
  		1.1 current.left != null => push
  		1.2 current.right != null => push
  		1.3 otherwise pop() and print()
  case2: pre == current.left
  		2.1 current.right 1= null => push
  		2.2 otherwise print 
  case3: pre == current.right  
  		pop() and print()
  
  
  public void postOrder(TreeNode root) {
  	if (root == null) {
  		return;
  	}
  	
  	Deque<TreeNode> stack = new ArrayDeque<>();
  	stack.offerFirst(root);
  	TreeNode pre = null;
  	while (!stack.isEmpty()) {
      ListNode cur = stack.peekFirst();
  		// case 1
  		if (pre == null || cur == pre.left || cur == pre.right) {
  			if (cur.left != null) {
  				stack.offerFirst(cur.left);
  			} else if (cur.right != null) {
  				stack.offerFirst(cur.right);
  			} else {
  				TreeNode cur = stack.pollFirst();
  				System.out.println(cur);
  			}
  		}
  		
  		// case 2
  		else if (pre == cur.left) {
  			if (cur.right != null) {
  				stack.offerFirst(cur.right);
  			} else {
  				TreeNode cur = stack.pollFirst();
  				System.out.println(cur);
  			}
  		}
  		
  		// case 3 
  		else {
  				TreeNode cur = stack.pollFirst();
  				System.out.println(cur);
  		}
      
      pre = cur;
  	}
  	
  }
  
  ```

  ![image-20200720204721841](../../../Library/Application Support/typora-user-images/image-20200720204721841.png)



- Level-order
  - use a queue and maintain each level size
  - 常见问题：判断complete binary tree, check minheap property



### 基本知识点2: Tree 常见概念

**Balanced binary tree:** is commonly defined as a binary tree in which the height of the left and right subtrees of every node differ by 1 or less.

任意node的左右子树高度差不超过1



**Complete binary tree:** is a binary Tree in which every level, except the last, is completely filled, and all nodes are as far left as possible.

除了最后一层所有的节点都是满的，最后一层的节点全部靠左

- Complete binary tree is easy to serialize to array

- 孩子的index 和 parent 存在关系
  - 如果index从0开始的话
    - left child = 2i + 1, right child = 2i + 2
    - parent = (i -1) / 2     向下取整
  - 如果index 从1开始的话
    - left child = 2i, right child = 2i + 1
    - parent = i / 2      向下取整



**Binary search tree:** left sub tree < for every single node < right sub tree

Binary search tree 常常会和 inoder traverse 结合



Q1 getHeight()

```
1. ask from children
left height
right height

2. calculate in current level
 - max(left, right) + 1
 
3. return to parent

```



Q2 isBalanced()

```java
         3 (2)
    /         \
    4  (0)       5 (1)
               /      \ 
              1 (0)     2 (0)
              
1. ask from children
leftHeight = isBalanced(root.left) 
rightHeight = isBalanced(root.right)

2. calculate in current level
if (|leftHeight - rightHeight| > 1) {
		return false;
}
currentHeight = max(left, right) + 1

3. return to parent
return currentHeight


  
public boolean isBalanced(TreeNode root) {
  if (root == null) {
    return true;
  }
  return helper(root) != -1;
}

private int helper(TreeNode root) {
  //base case
  if (root == null) {
    return 0;
  }
  
  // -1 is for false (not balanced)
  int left = helper(root.left);
  if (left == -1) {
    return -1;
  }
  int right = helper(root.right);
  if (right == -1 || Math.abs(left - right) > 1) {
  	return -1;
  }
  return Math.max(left, right) + 1;
}
```



Q2 isSymmetric()

Q3 identical of two tree or not

- Two cases: 

  - case 1: swap: (a.left, b.right) && (a.right, b.left) 
  - case 2: not swap: (a.left, b.left) && (a.right, b.right)

  Case 1 || case 2

Time: 

​	recursion tree has O(height) level

​    for each node has 4 branches





Q3 search()

```java
public TreeNode search (TreeNode root, int target) {
  while (root != null) {
		if (root.key == target.key) {
      return root;
    }
    if (root.key < target.key) {
      root = root.right;
    } else {
      root = root.left;
    }
  }
  return null;
}
```

Tail recursion: 最后一步是recursion call. 所有的尾递归很容易转成iterative solution，避免stack overflow

Insert() in BST

```java
public TreeNode insert(TreeNode root, int target) {
  if (root == null) {
    return new TreeNode(target);
  }
  TreeNode cur = root;
	while (cur != null) {
    if (cur.key == target) {
      return cur;
    } 
    
    if (cur.key > target) {
      if (cur.left == null) {
        cur.left = new TreeNode(target);
        break;
      } 
      cur = cur.left;
    } else {
      if (cur.right == null) {
        cur.right = new TreeNode(target);
        break;
      }
      cur = cur.right;
    }
  }
  return root;
}

// 挂树！！ 很巧妙
public TreeNode insert (TreeNode root, int target) {
  if (root == null) {
    return new TreeNode (target);
  }
  if (root.key > target) {
    root.left = insert(root.left, target);
  } else if (root.key < target) {
    root.right = insert(root.right, target);
  }
  return root;
}
```

Delete in BST

4 Cases

Time: O(h), Space: O(h)









merge two tree

```java
public TreeNode mergeTree(TreeNode t1, TreeNode t2) {
	TreeNode newNode = null;
	if (t1 == null && t2 == null) {
		return newNode;
	}
  
	if (t1 == null) {
		newNode = new TreeNode(t2.key);
	} else if (t2 == null) {
		newNode = new TreeNode(t1.key);
	} else {
		newNode = new TreeNode(t1.key + t2.key);
	}
	newNode.left = mergeTree(t1.left == null ? null : t1.left, t2.left == null ? null : t2.left);
	newNode.right = mergeTree(t1.right == null ? null : t1.right, t2.right == null ? null : t2.right);
	return newNode;
}
```





