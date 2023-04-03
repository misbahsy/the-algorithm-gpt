[View code on GitHub](https://github.com/misbahsy/the-algorithm/recos-injector/server/src/main/scala/com/twitter/recosinjector/event_processors/TweetEventProcessor.scala)

The `TweetEventProcessor` class is an event processor for the `tweet_events` EventBus stream from Tweetypie. This stream provides all the key events related to a new tweet, like Creation, Retweet, Quote Tweet, and Replying. It also carries the entities/metadata information in a tweet, including @ Mention, HashTag, MediaTag, URL, etc.

The purpose of this class is to process the incoming tweet events and convert them into two different graphs: UserUserGraph and UserTweetEntityGraph. These graphs are then published to Kafka topics for further processing.

The class contains several private methods that are used to extract information from the incoming tweet events. For example, `getTweetAction` method is used to determine the type of tweet (Tweet, Retweet, Quote, or Reply) based on the tweet details. Another method, `getFollowedByIds`, is used to get the list of users who actually follow the source user.

The class also contains several counters and filters that are used to track the processing of tweet events. For example, `numUrlCounter` and `numMediaUrlCounter` are used to track the number of URLs and media URLs in the tweet, respectively. `engageUserFilter` and `tweetFilter` are used to filter out unsafe users and tweets.

The `processEvent` method is the main method of the class that processes the incoming tweet events. It first extracts the tweet details using the `getTweetDetails` method and then checks if the tweet event should be processed using the `shouldProcessTweetEvent` method. If the tweet event passes the safety filters, it is converted into UserUserGraph and UserTweetEntityGraph and published to Kafka topics.

Overall, the `TweetEventProcessor` class plays a crucial role in processing the incoming tweet events and converting them into graphs for further processing.
## Questions: 
 1. What is the purpose of this code and what does it do?
- This code is an event processor for the tweet_events EventBus stream from Tweetypie. It processes key events related to a new tweet, such as creation, retweet, quote tweet, and replying. It also carries the entities/metadata information in a tweet, including @ Mention, HashTag, MediaTag, URL, etc.

2. What external dependencies does this code have?
- This code has external dependencies on several libraries, including Finagle, Frigate, Gizmoduck, Scrooge, and Tweetypie. It also uses a KafkaEventPublisher and a SocialGraph.

3. What are some of the statistics being tracked by this code?
- This code tracks several statistics related to tweet events, including the number of tweet create events, non-tweet create events, URL mentions, media URL mentions, hashtags, mentions, mediatags, valid mentions, valid mediatags, null cast tweets, null cast source tweets, fail safety levels, unsafe authors, processed tweets, and unprocessed tweets. It also tracks the number of self-retweets.