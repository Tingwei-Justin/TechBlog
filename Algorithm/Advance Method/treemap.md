239. Sliding Window Maximum

     - Method 1: use a treemap to record the sliding window

     ```java
         public int[] maxSlidingWindow(int[] nums, int k) {
             TreeMap<Integer, Integer> map = new TreeMap<>();
             for (int i = 0; i < k; ++i) {
                 map.put(nums[i], map.getOrDefault(nums[i], 0) + 1);
             }
             
             int[] result = new int[nums.length - k + 1];
             result[0] = map.lastKey();
             
             for (int i = 1; i < result.length; ++i) {
                 // remove left number
                 int leftCount = map.get(nums[i - 1]);
                 leftCount--;
                 if (leftCount == 0) {
                     map.remove(nums[i-1]);
                 } else {
                     map.put(nums[i-1], leftCount);
                 }
                 
                 // add right number
                 map.put(nums[i + k - 1], map.getOrDefault(nums[i + k - 1], 0) + 1);
                 
                 result[i] = map.lastKey();
             } 
             return result;
         }
     ```

     

     - Method 2: use a deque to to record the sliding window

     

     we only keep potential result.

     又大又新！（remain big and new) and remove old and small

     when new element comes in

     - if ele > queue.right  => remove deque.right until ele < queueright or deque is Empty()
     - otherwise deque.add(ele)
     - the current max value is deque.left

     

     

     ```
     [1,3,-1,-3,5,3,6,7]
     
     [5 ,3]
     ```

     

240. Scan line