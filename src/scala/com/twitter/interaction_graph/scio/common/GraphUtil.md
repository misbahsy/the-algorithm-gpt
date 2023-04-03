[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/scala/com/twitter/interaction_graph/scio/common/GraphUtil.scala)

The `GraphUtil` object contains utility methods for converting different types of edges into a common `InteractionGraphRawInput` class, as well as methods for filtering edges based on certain criteria. These methods are likely used in the larger project to preprocess and clean the data before feeding it into the main algorithm.

The `getFlockFeatures` method takes an `SCollection` of `FlockEdge` objects, a `FeatureName` enum, and the current time in milliseconds as input. It converts each `FlockEdge` into an `InteractionGraphRawInput` object, which contains the source and destination IDs, the feature name, the age of the edge in days, and a weight of 1.0. The age is calculated by taking the difference between the current time and the `updatedAt` field of the `FlockEdge`, which is in seconds. The resulting `SCollection` of `InteractionGraphRawInput` objects is returned.

The `getSocialGraphFeatures` method is similar to `getFlockFeatures`, but takes an `SCollection` of `SocialGraphEdge` objects instead. It also converts each edge into an `InteractionGraphRawInput` object, using the same age calculation as `getFlockFeatures`.

The `isFollow` method takes an `Edge` object as input and returns a boolean indicating whether the edge represents a follow relationship. It does this by checking if the `NumFollows` feature has a mean value of 1.0.

The `filterExtremes` method takes an `Edge` object as input and returns a boolean indicating whether the edge should be filtered out. It does this by checking if the edge weight is NaN, infinite, negative, or equal to the maximum value of `Double`. If any of these conditions are true, the method increments a corresponding counter and returns false. Otherwise, it returns true.

The `filterNegative` method takes an `Edge` object as input and returns a boolean indicating whether the edge should be filtered out. It does this by checking if any of the features in the `HEALTH_FEATURE_LIST` have a mean value greater than 0.0. If any of these conditions are true, the method returns false. Otherwise, it returns true.

Overall, the `GraphUtil` object provides useful utility methods for preprocessing and cleaning edge data in the larger project. The `getFlockFeatures` and `getSocialGraphFeatures` methods convert different types of edges into a common format, while the `isFollow`, `filterExtremes`, and `filterNegative` methods filter out edges based on certain criteria. These methods likely play a crucial role in preparing the data for the main algorithm to run on.
## Questions: 
 1. What is the purpose of the `GraphUtil` object?
- The `GraphUtil` object contains methods for converting different types of edges into a common `InteractionGraphRawInput` class, as well as methods for filtering edges based on certain criteria.

2. What is the significance of the `FeatureName` parameter in the `getFlockFeatures` and `getSocialGraphFeatures` methods?
- The `FeatureName` parameter specifies the type of feature that is being extracted from the edges, which is used to populate the `featureName` field in the resulting `InteractionGraphRawInput` objects.

3. What is the purpose of the `filterNegative` method?
- The `filterNegative` method filters out edges that have negative values for any of the features in the `HEALTH_FEATURE_LIST` constant, which is a list of features related to user health.