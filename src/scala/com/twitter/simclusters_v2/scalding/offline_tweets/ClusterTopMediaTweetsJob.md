[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/scala/com/twitter/simclusters_v2/scalding/offline_tweets/ClusterTopMediaTweetsJob.scala)

The code provided contains three objects: `ClusterTopTweetsJob`, `ClusterTopMediaTweets20M145K2020BatchJob`, and `AdhocClusterTopMediaTweetsJob`. 

`ClusterTopTweetsJob` contains a method `getClusterTopMediaTweets` that takes in a `TypedPipe` of persistent tweet embeddings and a `TypedPipe` of tweets, and returns a `TypedPipe` of tuples containing a `DayPartitionedClusterId` and a sequence of `(TweetId, Double)` tuples. The method first filters the tweets to only include those that contain media, and then joins this with the persistent embeddings to get the cluster ID and score for each tweet. It then maps this to a tuple containing the day partition and the tweet ID and score, and sums by key to get the top tweets for each cluster and day partition. Finally, it maps the result to a `DayPartitionedClusterId` and the sequence of top tweets for that cluster and day partition.

`ClusterTopMediaTweets20M145K2020BatchJob` is a scheduled job that runs every few hours and reads 21 days of tweets and the most recent persistent tweet embeddings from a Manhattan dump. It then calls `ClusterTopTweetsJob.getClusterTopMediaTweets` to get the top media tweets for each cluster and day partition, and writes the result to a DAL versioned key-value store.

`AdhocClusterTopMediaTweetsJob` is an adhoc debugging job that uses the entity embeddings dataset to infer user interests. It reads the same data as `ClusterTopMediaTweets20M145K2020BatchJob` and calls `ClusterTopTweetsJob.getClusterTopMediaTweets` to get the top media tweets for each cluster and day partition. It then calls `ClusterTopTweetsJob.analyzeClusterResults` to perform some statistical analysis on the results, such as the number of tweets in a cluster and tweet score distributions. Finally, it writes the result to a TSV file.

Overall, these objects are used to extract the top media tweets for each cluster and day partition from a large dataset of tweets and persistent embeddings. This information can be used for various purposes, such as recommending media content to users based on their interests.
## Questions: 
 1. What is the purpose of the `ClusterTopTweetsJob` object?
- The `ClusterTopTweetsJob` object contains functions for processing tweet data and generating a clusterId-> List[tweetId] index.

2. What is the purpose of the `ClusterTopMediaTweets20M145K2020BatchJob` object?
- The `ClusterTopMediaTweets20M145K2020BatchJob` object is a scheduled job that runs every couple of hours, reads 21 days of tweets and the most recent persistent tweet embeddings from a Manhattan dump, and outputs a clusterId-> List[tweetId] index.

3. What is the purpose of the `AdhocClusterTopMediaTweetsJob` object?
- The `AdhocClusterTopMediaTweetsJob` object is an adhoc debugging job that uses Entity Embeddings dataset to infer user interests and runs some stat analysis on the results, such as the number of tweets in a cluster, tweet score distributions, etc.