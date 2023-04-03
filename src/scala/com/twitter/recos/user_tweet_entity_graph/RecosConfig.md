[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/scala/com/twitter/recos/user_tweet_entity_graph/RecosConfig.scala)

The `RecosConfig` object holds all the configuration parameters for the recommendation graph used in the Twitter recommendation system. The configuration parameters are used to build a bipartite graph that represents the relationship between users and tweets. The graph is built using the `NodeMetadataLeftIndexedPowerLawMultiSegmentBipartiteGraphBuilder` class from the `com.twitter.recos.graph_common` package.

The configuration parameters include the maximum number of segments, maximum number of edges per segment, expected number of left nodes (users), expected maximum left degree (maximum number of tweets a user can have), left power law exponent (degree distribution of left nodes), expected number of right nodes (tweets), and number of right node metadata types (hashtag and URL). These parameters are used to configure the `GraphBuilderConfig` object, which is passed to the `NodeMetadataLeftIndexedPowerLawMultiSegmentBipartiteGraphBuilder` class to build the bipartite graph.

In addition to the graph configuration parameters, the `RecosConfig` object also includes other parameters such as the maximum size of user and tweet social proof, maximum tweet age, and maximum engagement age. These parameters are used in the recommendation algorithm to filter out tweets that are too old or have too little social proof.

The `println` statements at the end of the object are used to print out the configuration parameters when the object is initialized.

Example usage:
```
val config = RecosConfig
val graphBuilder = new NodeMetadataLeftIndexedPowerLawMultiSegmentBipartiteGraphBuilder(config.graphBuilderConfig)
val graph = graphBuilder.build()
```
## Questions: 
 1. What is the purpose of the `RecosConfig` object?
- The `RecosConfig` object holds all the configuration parameters for the `recos graph`.

2. What is the significance of the `maxNumSegments` and `maxNumEdgesPerSegment` variables?
- `maxNumSegments` and `maxNumEdgesPerSegment` determine the maximum number of segments and edges per segment that the graph can have respectively.

3. What are the different types of node metadata that are supported by the graph?
- The graph supports two types of node metadata: hashtag and url.