[View code on GitHub](https://github.com/misbahsy/the-algorithm/follow-recommendations-service/common/src/main/scala/com/twitter/follow_recommendations/common/utils/RandomUtil.scala)

The `RandomUtil` object provides three methods for weighted random sampling and shuffling of sequences. These methods are useful for generating random samples from a given sequence, where each element in the sequence has a weight associated with it. The weights can be used to control the probability of an element being selected in the sample.

The first method, `weightedRandomSamplingWithReplacement`, takes a sequence of items and a function that provides the weight for each item. It returns an infinite stream of items that are sampled with replacement using the weights. The method checks that all weights are non-negative and that the sum of weights is positive. If the sequence is empty, an empty stream is returned. The method uses the cumulative probability distribution to sample the items. The probability of an item being selected is proportional to its weight.

The second method, `weightedRandomShuffle`, takes a sequence of items and their weights and returns a lazy weighted shuffle of the elements in the list. The method checks that all weights are positive. The method uses the cumulative weight distribution to shuffle the items. The probability of an item being selected is proportional to its weight.

The third method, `weightedRandomShuffleByRank`, takes a sequence of items and a weight function that is based on the rank of the element in the original list. It returns a lazy weighted shuffle of the elements in the list. The method first creates a sequence of pairs, where each pair contains an item and its weight based on its rank. It then calls the `weightedRandomShuffle` method with this sequence and maps the resulting stream to the original items.

These methods can be used in various applications where random sampling or shuffling is required. For example, they can be used in recommendation systems to generate random recommendations based on the weights of the items. They can also be used in machine learning algorithms to generate random training or test sets based on the weights of the samples. 

Example usage:

```scala
case class Item(name: String, weight: Double)

implicit val itemWeighted: Weighted[Item] = (item: Item) => item.weight

val items = Seq(Item("A", 0.2), Item("B", 0.3), Item("C", 0.5))

// Weighted random sampling with replacement
val sample = RandomUtil.weightedRandomSamplingWithReplacement(items).take(5).toList
// Output: List(Item(C,0.5), Item(C,0.5), Item(B,0.3), Item(C,0.5), Item(C,0.5))

// Weighted random shuffle
val shuffled = RandomUtil.weightedRandomShuffle(items).take(3).toList
// Output: List(Item(C,0.5), Item(B,0.3), Item(A,0.2))

// Weighted random shuffle by rank
val shuffledByRank = RandomUtil.weightedRandomShuffleByRank(items, (rank: Int) => 1.0 / (rank + 1)).take(3).toList
// Output: List(Item(C,0.5), Item(B,0.3), Item(A,0.2))
```
## Questions: 
 1. What is the purpose of the `weightedRandomSamplingWithReplacement` function?
- The function takes a sequence of items with weights and returns an infinite stream that is sampled with replacement using the weights for each item. The weights must be greater than or equal to zero, and the sum of weights should be greater than zero.

2. What is the difference between `weightedRandomShuffle` and `weightedRandomShuffleByRank`?
- `weightedRandomShuffle` takes a sequence of items and their weights and returns a lazy weighted shuffle of the elements in the list. All weights should be greater than zero. On the other hand, `weightedRandomShuffleByRank` takes a sequence of items and a weight function based on the rank of the element in the original list.

3. What is the purpose of the `implicit weighted: Weighted[T]` parameter in the functions?
- The `implicit weighted: Weighted[T]` parameter is used to provide weights for the items in the sequence. It is an implicit parameter, which means that the compiler will automatically look for an instance of the `Weighted` type class for the type `T`.