Summary the idea of array problems



### Use prefix idea

Maximum Size Subarray Sum Equals k

- Naive solution 1:

  calculate the prefix first, and then calculate each possible subarray sum by sum[j] - sum[i] + num[i]

  time: O(n^2)

  Space: O(n)

- prefix + hashtable

  idea: we calculate the prefix and at the same time we calculate the subarray sum

  we use hashtable to record previous prefix sum and its first ending index

  [1, 3, 2, 4]

  according to: `sum - (sum - k) == k`

  for ( i = 0 : length) {

  ​	prefixSum += num[i];

  ​	check (prefixSum - k) in hashtable or not

  ​	if exist:

  ​		update the max

  ​	if (prefixSum not in map) {

  ​		map.put()	

  ​	}

  }

  ```java
  private int solutionWithHashTable(int[] nums, int k) {
      if (nums == null || nums.length == 0) {
        return 0;
      }
      // hashmap record the each prefix sum and its first ending index sum [0...i]
      HashMap<Integer, Integer> prefixSumMap = new HashMap<>();
      int max = 0;
      int prefixSum = 0;
      // ⚠️ 我们需要添加base case 没有元素的时候 prefix sum = 0, index = -1
      prefixSumMap.put(0, -1);
      // sum - (sum - k) = k
      for (int i = 0; i < nums.length; i++) {
        prefixSum += nums[i];
        int j = prefixSumMap.getOrDefault(prefixSum - k, Solution.INVALID_NUM);
        if (j != Solution.INVALID_NUM) {
          max = Math.max(i - j, max);
        } 
        if (!prefixSumMap.containsKey(prefixSum))
          prefixSumMap.put(prefixSum, i);
      }
      return max;
  }
  ```

  similar question:

  1. Given an array *nums* and a target value *k*, find the totoal number of subarrays that sums to *k*.