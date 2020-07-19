面试算法中常见的deep copy问题常见有以下两种，copy一个list 或者 一个graph。

- Deep copy List 

- Deep copy graph

  

这类问题的解决思路是一边遍历一边copy，但是要注意每一个node只copy一次，所以在一些复杂的情况我们需要借助hashmap来保证origin node 和copy node的映射关系， 通过hashmap可以避免出现一个node 被复制多次的情况



> 题目： Each of the nodes in the linked list has another pointer pointing to a random node in the list or null. Make a deep copy of the original list.

### Deep copy list with random pointer

```java 
// time: O(n)
// space: O(n)
public ListNode deepCopyList(ListNode head) {
	//conner case
	if (head == null) {
		return null;
	}
	
	HashMap<ListNode, ListNode> map = new HashMap<>();
	ListNode dummy = new ListNode(-1);
	ListNode cur = dummy;
	
	while(head != null) {
		//copy head
		if (!map.containsKey(head)) {
			map.put(head, new ListNode(head.value));
		}	
		cur.next = map.get(head);
		
		// copy head.random
		if (head.random != null) {
			if (!map.containsKey(head.random) {
				map.put(head.random, new ListNode(head.random.value);
			}
			cur.next.random = map.get(head.random);
		}
		
		head = head.next;
		cur = cur.next
	}
	
	return dummy.next;
}
```



###  Deep copy graph

在deep copy 图的时候通常会有两种复制方式。

Method 1: 直接利用graph的表示方式（adjacent matrix or adjacent List)， 通过遍历list来复制。

Method 2: 如果graph只给我们了第一个node, 就需要去traverse （bfs/dfs) 整个graph来复制。

无论哪种方式，我们都需要将original node    <->  copy node的映射关系存在hashmap中。避免重复复制

```java
/*
* class GraphNode {
*   public int key;
*   public List<GraphNode> neighbors;
*   public GraphNode(int key) {
*     this.key = key;
*     this.neighbors = new ArrayList<GraphNode>();
*   }
* }
*/

// method 1 directly copy the graph through adjacent list.
public List<GraphNode> deepCopyGraph(List<GraphNode> graph) {
  HashMap<GraphNode, GraphNode> map = new HashMap<>();
  
  for (GraphNode cur : graph) {
    GraphNode newNode = getOrCreate(cur, map);
    for (GraphNode nei : cur.neighbors) {
      GraphNode newNeighor = getOrCreate(nei, map);
      newNode.neighbors = newNeighbor;
    }
  }
  return new ArrayList<>(map.values());
}

private GraphNode getOrCreate(GraphNode node, HashMap<GraphNode, GraphNode> map) {
  if (!map.containsKey(node)) {
    map.put(node, new GraphNode(node.key));
  }
  return map.get(node);
}
```

```java
// method 2 copy by traversing the graph(dfs)

public List<GraphNode> deepCopyGraph(List<GraphNode> graph) {
  HashMap<GraphNode, GraphNode> map = new HashMap<>();
  
  for (GraphNode node : graph) {
    dfs(node, map);
  }
  return new ArrayList(map.values());
}

private GraphNode dfs(GraphNode node, HashMap<GraphNode, GraphNode> map) {
  if (map.containsKey(node)) {
    return map.get(node);
  }
  GraphNode copy = new GraphNode(node.key)
  map.put(node, copy);
  for (GraphNode nei : node.neighbors) {
    copy.neighbors.add(dfs(nei, map));
  }
  return copy;
}
```



