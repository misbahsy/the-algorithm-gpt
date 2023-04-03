[View code on GitHub](https://github.com/misbahsy/the-algorithm/follow-recommendations-service/server/src/main/scala/com/twitter/follow_recommendations/flows/post_nux_ml/PostNuxMlCombinedRankerBuilder.scala)

The `PostNuxMlCombinedRankerBuilder` class is used to build a combined ranker that comprises four stages of ranking. The purpose of this code is to provide a way to rank candidate users for follow recommendations on Twitter. The four stages of ranking are:

1. Weighted sampler: This stage samples from the candidate sources based on their weights.
2. Truncating to the top N merged results for ranking: This stage takes the first N results while merging duplicates.
3. ML ranker: This stage uses a machine learning model to score the candidates.
4. Interleaving ranker for producer-side experiments: This stage combines rankings from several rankers and enforces candidates' ranks in experiment buckets according to their assigned ranker model.
5. Impression-based fatigueing: This stage uses impressions to fatigue the candidates.

The `build` method constructs each ranker independently and chains them together. It takes a request object and a map of candidate source weights as input and returns a `Ranker` object that can be used to rank candidate users. The `buildMainRanker`, `buildInterleaveRanker`, and `buildFatigueRanker` methods are helper methods that build the main ranker, interleave ranker, and fatigue ranker, respectively.

The `PostNuxMlCombinedRankerBuilder` class uses several other classes and interfaces from the `com.twitter.follow_recommendations` and `com.twitter.product_mixer` packages, such as `IdentityRanker`, `IdentityTransform`, `MlRanker`, `HydrateFeaturesTransform`, `WeightedCandidateSourceRanker`, `InterleaveRanker`, `ImpressionBasedFatigueRanker`, and more. These classes and interfaces provide the functionality needed to build the ranker.

Here is an example of how the `PostNuxMlCombinedRankerBuilder` class can be used:

```scala
val builder = new PostNuxMlCombinedRankerBuilder(request, candidateSourceWeights)
val ranker = builder.build()
val rankedCandidates = ranker.rank(candidates)
```
## Questions: 
 1. What is the purpose of this code and what problem does it solve?
- This code builds a combined ranker for post-NUX follow recommendations on Twitter. It comprises 4 stages of ranking: weighted sampler, truncating to the top N merged results for ranking, ML ranker, and interleave ranker for producer-side experiments, and impression-based fatigueing. The purpose is to provide a ranked list of recommended users to follow for a given user.

2. What dependencies does this code have?
- This code has dependencies on several other packages and classes, including `com.twitter.finagle.stats.StatsReceiver`, `com.twitter.follow_recommendations.common.base`, `com.twitter.follow_recommendations.common.feature_hydration.common`, `com.twitter.follow_recommendations.common.models`, `com.twitter.follow_recommendations.common.rankers.common`, `com.twitter.follow_recommendations.common.rankers.fatigue_ranker`, `com.twitter.follow_recommendations.common.rankers.first_n_ranker`, `com.twitter.follow_recommendations.common.rankers.interleave_ranker`, `com.twitter.follow_recommendations.common.rankers.ml_ranker.ranking`, `com.twitter.follow_recommendations.common.rankers.weighted_candidate_source_ranker`, `com.twitter.follow_recommendations.configapi.candidates`, `com.twitter.product_mixer.core.model.common.identifier`, `com.twitter.product_mixer.core.model.marshalling.request`, `com.twitter.timelines.configapi`, and others.

3. What are the conditions under which the heavy-ranker is disabled?
- The heavy-ranker is disabled for users not bucketed due to empty results from the new candidate source. It is also disabled for requests with experimental heavy-rankers.