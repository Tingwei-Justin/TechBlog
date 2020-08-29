\218. The Skyline Problem

![image-20200827002103853](../../../../Library/Application Support/typora-user-images/image-20200827002103853.png)

The main idea of the solutions is to keep an eye on the max height of buildings, and whenever the max height changes, we add it to a list.

Each rectangle can view as two different event.

1. Insert a line 
2. Remove a line

We sort the event by x position, and we scan sorted event from left to right. Output each moment highest height.

for each events:

​		1. insert a line

​		2. remove a line

​		3. get the max height from current line

I use treemap because it can provide good performance for those three operations.

Use a TreeMap to record the valid line height and its count <Key: height, Value: count>



Consider conner case:

Case1: if current max height == last max height    ==> merge it to one (ignore the last)

Case 2: if current.x == last_result.x  ==> remove last_result, and then update the latest 

```java
class Solution {
    public List<List<Integer>> getSkyline(int[][] buildings) {
        List<List<Integer>> result = new ArrayList<>();
        ArrayList<Event> events = new ArrayList<>();
        for (int[] building : buildings) { // O(n)
            events.add(new Event(1, building[0], building[2])); //left border
            events.add(new Event(-1, building[1], building[2])); // right border
        }
        
        events.sort(Comparator.comparingInt((Event e) -> e.x)); // O(logn * n)
        TreeMap<Integer, Integer> map = new TreeMap<>();
        // key: height, value: number of current event with height
        
        for (Event e : events) { // O(n * log n)
            // 1. update the treemap
            if (e.flag == 1) {
                map.put(e.h, map.getOrDefault(e.h, 0) + 1);
            } else {
                int curCount = map.get(e.h);
                curCount--;
                if (curCount == 0) {
                    map.remove(e.h);
                } else {
                    map.put(e.h, curCount);
                }
            }
            
            // case 1: if current event left position == last result left position => remove last
            if (!result.isEmpty() && e.x == result.get(result.size() - 1).get(0)) {
                result.remove(result.size() - 1);
            }
            // case 2: if current event height == last result height => ignore current event
						
    
            int curMax = map.isEmpty() ? 0 : map.lastKey();
            if (result.isEmpty() || curMax != result.get(result.size() - 1).get(1)) {
                List<Integer> cur = Arrays.asList(new Integer[] {e.x, curMax});
                result.add(cur);
            }
        }
        return result;
    }
    
    public static class Event {
        int flag;
        int x;
        int h;
        public Event(int flag, int x, int h) {
            this.flag = flag;
            this.x = x;
            this.h = h;
        }
    }
}
```







```
0 1 2 3 4 5 6 7
2 1 2 1 2 1 2 1
dp[2][3] = 1
dp[4][5] = 1 + 1
dp[6][7] = 1 + 2 = 3

for（int i = 1; i < n; ++i) {
	for (int j = i; j < n; ++j) {
	
	
	}

}

 1 1 1 1
   1 1
    1
```

