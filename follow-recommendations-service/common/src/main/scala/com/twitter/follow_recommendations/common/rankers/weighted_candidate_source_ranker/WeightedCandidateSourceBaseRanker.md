[View code on GitHub](https://github.com/misbahsy/the-algorithm/follow-recommendations-service/common/src/main/scala/com/twitter/follow_recommendations/common/rankers/weighted_candidate_source_ranker/WeightedCandidateSourceBaseRanker.scala)

The `WeightedCandidateSourceBaseRanker` class is a ranker that selects the next candidate source to select a candidate from. It supports two kinds of algorithms: WeightedRandomSampling or WeightedRoundRobin. WeightedRandomSampling picks the next candidate source randomly, while WeightedRoundRobin picks the next candidate source sequentially based on the weight of the candidate source. It is default to WeightedRandomSampling if no weight method is provided.

The class takes in a set of candidate sources and their weights, and returns a stream of candidates. The `stream` method creates an iterator over algorithms and calls next to return a Stream of candidates. The method takes in the set of candidate sources that are being sampled, a map of candidate source to weight, the map of candidate source to the iterator of its results, and a weight method. When WeightedRandomSampling is set, the next candidate is picked from a candidate source that is randomly chosen. When WeightedRoundRobin is set, the next candidate is picked from the current candidate source until the number of candidates reaches the assigned weight of the candidate source. The next call of this function will return a candidate from the next candidate source which is after the previous candidate source based on the order input candidate source sequence.

The `apply` method takes in a map of candidate sources to their recommendations and returns a stream of candidates. It calls the `stream` method with the set of candidate sources, their weights, and an iterator over their recommendations.

Example usage of this class:

When using WeightedRandomSampling:
```
val ranker = new WeightedCandidateSourceBaseRanker[String, String](
  Map("CS1" -> 3, "CS2" -> 2, "CS3" -> 5),
  WeightedRandomSampling,
  None
)
val input = Map(
  "CS1" -> List("CS1_candidate1", "CS1_candidate2", "CS1_candidate3", "CS1_candidate4", "CS1_candidate5"),
  "CS2" -> List("CS2_candidate1", "CS2_candidate2", "CS2_candidate3", "CS2_candidate4", "CS2_candidate5", "CS2_candidate6"),
  "CS3" -> List("CS3_candidate1", "CS3_candidate2", "CS3_candidate3", "CS3_candidate4", "CS3_candidate5")
)
val output = ranker(input).take(20).toList
```
Ranked candidates sequence is not determined because of random sampling. One possible output candidate sequence is: (CS1_candidate1, CS2_candidate1, CS2_candidate2, CS3_candidate1, CS3_candidates2, CS3_candidate3, CS1_candidate2, CS1_candidate3, CS3_candidate4, CS3_candidate5, CS1_candidate4, CS1_candidate5, CS2_candidate6, CS2_candidate3,...)

When using WeightedRoundRobin:
```
val ranker = new WeightedCandidateSourceBaseRanker[String, String](
  Map("CS1" -> 3, "CS2" -> 2, "CS3" -> 5),
  WeightedRoundRobin,
  None
)
val input = Map(
  "CS1" -> List("CS1_candidate1", "CS1_candidate2", "CS1_candidate3", "CS1_candidate4", "CS1_candidate5"),
  "CS2" -> List("CS2_candidate1", "CS2_candidate2", "CS2_candidate3", "CS2_candidate4", "CS2_candidate5", "CS2_candidate6"),
  "CS3" -> List("CS3_candidate1", "CS3_candidate2", "CS3_candidate3", "CS3_candidate4", "CS3_candidate5")
)
val output = ranker(input).take(20).toList
```
Output candidate sequence is: (CS1_candidate1, CS1_candidate2, CS1_candidate3, CS2_candidate1, CS2_candidate2, CS3_candidate1, CS3_candidate2, CS3_candidate3, CS3_candidate4, CS3_candidate5, CS1_candidate4, CS1_candidate5, CS1_candidate1, CS2_candidate3,...)
## Questions: 
 1. What is the purpose of this code and how is it used?
- This code is a ranker that selects the next candidate source to select a candidate from. It supports two kinds of algorithm, WeightedRandomSampling or WeightedRoundRobin. It is used to generate a stream of candidates based on the input candidate sources and their weights.

2. What are the inputs and outputs of the `stream` method?
- The inputs of the `stream` method are `candidateSources` (a set of candidate sources that are being sampled), `candidateSourceWeights` (map of candidate source to weight), `candidates` (map of candidate source to the iterator of its results), `weightMethod` (an enum to indicate which weight method to use), and `random` (an optional random seed). The output of the `stream` method is a stream of candidates.

3. What is the purpose of the `Weighted` trait and how is it used?
- The `Weighted` trait is used to define a function that takes an input of type `A` and returns a `Double` value representing the weight of that input. It is used to define the weight of each candidate source in the `stream` method.