[View code on GitHub](https://github.com/misbahsy/the-algorithm/timelineranker/server/src/main/scala/com/twitter/timelineranker/util/SourceTweetsUtil.scala)

The `SourceTweetsUtil` object provides utility methods for extracting source tweet IDs from a sequence of `ThriftSearchResult` objects. These methods are used to identify tweets that are relevant to a particular user or set of users, based on various criteria such as retweets, replies, and mentions.

The `getSourceTweetIds` method is the main entry point for this utility, and takes several parameters including the search results, a set of tweet IDs, a sequence of followed user IDs, a boolean flag indicating whether to include reply root tweets, and a `StatsReceiver` object for tracking metrics. This method calls several other methods to extract the relevant tweet IDs based on the input criteria, and returns a sequence of distinct tweet IDs.

The `getInNetworkInReplyToTweetIds` method extracts tweet IDs for in-network replies to followed users. It takes the search results, a set of tweet IDs, and a sequence of followed user IDs as input parameters, and returns a sequence of tweet IDs that are not already in the input set.

The `getReplyRootTweetIds` method extracts tweet IDs for reply root tweets. It takes the search results and a set of tweet IDs as input parameters, and returns a sequence of tweet IDs that are not already in the input set.

The `getRetweetSourceTweetIds` method extracts tweet IDs for retweets. It takes the search results and a set of tweet IDs as input parameters, and returns a sequence of tweet IDs that are not already in the input set.

The `getExtendedReplySourceTweetIds` method extracts tweet IDs for extended replies to followed users. It takes the search results, a set of tweet IDs, and a sequence of followed user IDs as input parameters, and returns a sequence of tweet IDs that are not already in the input set.

Overall, these utility methods are used to identify relevant tweets for a particular user or set of users, based on various criteria such as retweets, replies, and mentions. These tweet IDs can then be used to construct a timeline or other view of the relevant tweets.
## Questions: 
 1. What is the purpose of this code?
    - This code provides utility functions for extracting tweet IDs from search results based on various criteria.

2. What are the input parameters for the `getSourceTweetIds` function?
    - The input parameters are `searchResults` (a sequence of `ThriftSearchResult` objects), `searchResultsTweetIds` (a set of `TweetId` objects), `followedUserIds` (a sequence of `UserId` objects), `shouldIncludeReplyRootTweets` (a boolean flag), and `statsReceiver` (a `StatsReceiver` object).

3. What is the purpose of the `replyRootTweetCounter` variable?
    - The `replyRootTweetCounter` variable is a counter that keeps track of the number of reply root tweets that are included in the final output. It is incremented by the size of the `rootTweetIds` sequence if `shouldIncludeReplyRootTweets` is true.