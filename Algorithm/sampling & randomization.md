## 洗牌问题（shuffling) 

如何随机洗牌，保证每一张牌概率相同

这类题目的思路：从没有选过的牌中随机选一个，并跟左边交换，始终位置左边是选好的，右边是为选好的顺序，这么做的目的是方便使用random函数。

```
idea:

1, 2, 3, 4, 5, 6 ... 54
[0, i): shuffled cards
[i, 53]: unshuffled cards

for each steps
	1. randomly pick 1 non-shuffled card (cards[j])
  2. swap card[i], card[j]
  3. i++
```

```java
// code
for (int i = 0; i < cards.length; i++) {
  int j = random.nextInt(cards.length - i) + i;
  swap(cards, i++, j);
}
```

**Prove :**

first round: 1/54

second round:（53/54） * （1/53） = 1/54

third round:（53/54）* （52/53） * （1/52） = 1/54

...

All the round have the same probability (1/54)



根据这个思路，以下的变种问题都可以利用这个思路来解决

- Select random k elements in an array of size n
- get a k-permutation of an array of size n
- find all k-permutations of an array of size n



## 抽样问题（sampling) 

如果从stream data中随机返回1或k个数据，使得每次返回的数据概率相同（1/n 或 k/n)

首先我们需要明确什么是stream，stream可以理解为不知道一共有多少个数据，只知道是否有下一个数据，以及下一个数据是什么

```java
class Stream {
  // return null if the stream ends
  public Element getNext();
}
```

solution 1

```
store everything we already read, and call random(n)
Time: O(n)
Space: O(n)
```



Can we do better?       Space O(n)  -> O(1)



**Reservoir sampling** is a family of [randomized algorithms](https://en.wikipedia.org/wiki/Randomized_algorithm) for choosing a [simple random sample](https://en.wikipedia.org/wiki/Simple_random_sample) without replacement of *k* items from a population of unknown size *n* in a single pass over the items. The size of the population *n* is not known to the algorithm and is typically too large to fit all *n* items into [main memory](https://en.wikipedia.org/wiki/Main_memory). The population is revealed to the algorithm over time, and the algorithm cannot look back at previous items. At any point, the current state of the algorithm must permit extraction of a simple random sample without replacement of size *k* over the part of the population seen so far.

Solution 2

```java
The data structure we need:
1. count (int): how many elements I have read so far.
2. sample: the current randomly picked elements so far.

For each new element we read, we have k/count probability to replace sample with this new element
Round k+1: count = 1, replace prob = k/k + 1
Round k+2: count = 2, replace prob = k/k + 2
Round k+3: count = 3, replace prob = k/k + 3
...
Round n: count = n, replace prob = k/n


Jave Code
  
public Element getSample() {
  Element[] sample = new Element[k];
  int counter = 0;
  for (int i = 0; i < k; i++) {
    sample[i] = stream.getNext();
    counter++;
  }
  
	Element newElement = stream.getNext();
	while (newElement != null) {
		counter++;
    int rand = random.nextInt(counter);
		if (rand < k) { // k/count probability to replace the sample with new element
			sample[rand] = newElement;
		}
		newElement = stream.getNext();
	}
}
```



！！！ Follow up

返回随机最大的number

Case1: new element < max           =>          ignore 

Case2: new element == max 		=> 		reservior sampling

Case 3: new element > max 		=> 		max = new element, count = 1



## 随机问题 (randomization)

- 用Random5实现一个Random7
- 用Random2实现一个Random1,000,000



这种问题拿到之后看似有一些难度，但是我们反过来思考一下

如果给了Random 7(), 我们可以很容易获得Random 5(), 因为在每一个数字相同概率下，只要生成的数字小于等于5我们就可以留做结果。所以我们延伸一下这个思路，也就是说如果可以得到一个Random K(), K 只要大于等于我们需要的随机值，我们就可以很容易实现 Random <= K 的任何函数。

那么这就使得我们的思路转变为 如何用Random5实现一个  Random>=7的任何一个函数?

很简单，通过构造一个5进制的数来实现。

假设五进制有2 bits, 那么它的范围就是 0 <= x < 5^2 -1

假设五进制有3 bits, 那么它的范围就是 0 <= x < 5^3 - 1

.....

1          2           3

0 ~4    0 ~4    0~4

那我们具体取多少个bits取决于我们需要多少，只要 >= 我们的target值就好

以这道题目为例，只需要2bits，我们就可以大于7 （5^2 > 7)

```java
public int random7() {
	while (true) {
    int r = random5() + random5() * 5; // 通过random 5 构造一个0 ～ 24 的随机数
    if (r < 21) {
      return r % 7;
    }
  }
}
```



isSymtemitic(TreeNode left, TreeNode right) {

​	if (TreeNode left != TreeNode right) {

​		return true;   

​	}

​	return isSymtemitic(left.left, right.right) && isSymte

}



## 流数据问题（stream data)

- how to keep track of median of the numbers read so far?

  

