## Question: Minimum Window Substring

```
Given a string S and a string T, find the minimum window in S which will contain all the characters in T

Input: S = “ADOBECODEBANC”

          T = “ABC”

Output: “BANC”
```



```
High level idea: Use sliding window to solve this problem.

Use two pointers to maintain the sliding window [i, j]: represents the minimum window substring ending with j th chars of string S.

We also need two hashmap.
One hashmap <Character, Integer>: save the chars in target string, and its #
example:
T = “ABC”
 targetMap = {{A, 1}, {B, 1}, {C,1}}
 
 
Another HashMap <Character, Integer>: record the chars in S also in T and number of this char in current sliding window

example:

 S = “ADOBECODEBANC”
      ____
 
 windowMap = {{A, 1}, {B, 1}}
 
 
[left, right] to maintain current sliding window
[global left, global right] to global min sliding window

int match: the number of chars match the target

The key point: when we update the left and right pointer

Initial:
left = 0
right = 0
match = 0

“ADOBECODEBANC”

 ______
for (right = 0 to s.length ) {
	// update right pointer
	s[right] in targetMap {
		getCount from hashmap
		and count++;
		if (count <= targetMap.get(s[right])) {
			match++;
		}
	}
	
	if (match < target.length) {
		continue;
	}
	
	// update left pointer
	for (j = left; j <= right; j++) {
		if (s[j] in windowMap and count(s[j]) in slidingwindow == count(s[j]) in target) {
			left = j;
			break;
		}
	}
	
	// update global left and right
	if (gr - gl > r - l) {
		gr = r
		gl = l
	}
}

return source.substring(gl, gr + 1);
```



```java
public String findMinWindowSubstring(String source, String target) {
	if (target.length() > source.length()) {
		return "";
	}
  HashMap<Character, Integer> windowMap = new HashMap<>();
  HashMap<Character, Integer> targetMap = new HashMap<>();
  // initial the targetMap
  for (int i = 0; i < target.length(); i++) {
    char c = target.charAt(i);
    int count = targetMap.getOrDefault(c, 0);
    count++;
    targetMap.put(c, count);
  }
  int left = 0;
  int globalLeft = 0;
  int globalRight = -1;
  int match = 0;
  
  for (int right = 0; right < source.length(); right++) {
     //step1: update right
   	char c = source.charAt(right);
    int targetCount = targetMap.getOrDefault(c, -1);
    if (targetCount > 0) {
      int winCount = windowMap.getOrDefault(c, 0);
      windowMap.put(c, ++winCount);
      if (winCount <= targetCount) {
        match++;
      }
    }
    if (match < target.length()) {
      continue;
    }
    
    // step2: update left
    for (int i = left; i <= right; i++) {
      char lc = source.charAt(i);
      int lcCount = windowMap.getOrDefault(lc, -1);
      if (lcCount > 0 && lcCount == targetMap.get(lc)) {
        left = i;
        break;
      } else if (lcCount > 0 && lcCount > targetMap.get(lc)) {
        windowMap.put(lc, --lcCount);
      }
    }
    
    // step3: update global left and right
    if (globalRight - globalLeft > right - left) {
      globalRight = right;
      globalLeft = left;
    } 
  }
  return globalRight == -1 ? "" : source.substring(globalLeft, globalRight + 1);
}
```

### Longest Substring With K Typed Characters

Given a string, return the **longest contiguous substring** that contains **exactly** k type of characters.

Return null if there does not exist such substring.

Conner case: 

- no valid result返回什么， k == 0返回什么
- 注意初始化globalleft 和 globalright的default value

sliding window semantic

when to update right

when to update left

when to update the result

```java
public class Solution {
  // time: O(n)
  // space: O(k)
  public int lengthOfLongestSubstringKDistinct(String input, int k) {
    if (k == 0) {
      return 0;
    }
    int globalResult = 0;
    int left = 0;
    HashMap<Character, Integer> map = new HashMap<>();

    for (int right = 0; right < input.length(); right++) {
      // step 1: add current right to hashmap
      int rightCount = map.getOrDefault(input.charAt(right), 0);
      map.put(input.charAt(right), rightCount + 1);

      // step2: update left until map.size() <= k
      while (map.size() > k) {
        int leftCount = map.get(input.charAt(left));
        leftCount--;
        if (leftCount == 0) {
          map.remove(input.charAt(left));
        } else {
          map.put(input.charAt(left), leftCount);
        }
        left++;
      }
      
      // step3: update globalresult
      globalResult = Math.max(globalResult, right - left + 1);
    }
    return globalResult;
  }
}
```



### 382. Shortest Substring With K Typed Characters

Conner case: 

- no valid result返回什么， k == 0返回什么
- 注意初始化globalleft 和 globalright的default value

sliding window semantic

when to update right

when to update left

when to update the result