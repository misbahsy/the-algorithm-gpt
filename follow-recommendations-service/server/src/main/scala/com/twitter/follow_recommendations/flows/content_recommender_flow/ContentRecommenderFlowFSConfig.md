[View code on GitHub](https://github.com/misbahsy/the-algorithm/follow-recommendations-service/server/src/main/scala/com/twitter/follow_recommendations/flows/content_recommender_flow/ContentRecommenderFlowFSConfig.scala)

The `ContentRecommenderFlowFSConfig` class is a configuration file that defines the feature switches for the content recommender flow in the Twitter application. It extends the `FeatureSwitchConfig` class and overrides its methods to define the boolean, integer, and double feature switch parameters.

The boolean feature switch parameters are defined as a sequence of `Param[Boolean] with FSName` objects. These parameters control whether certain candidate sources are included in the content recommender flow, such as activity-based, social-based, geo-based, and home timeline tweet recommendations. They also control whether certain predicates are enabled, such as recent following, gizmoduck, inactive, and invalid target candidate relationship predicates. Additionally, there are parameters for including new following and more geo-based candidate sources, as well as for target eligibility and getting followers from Sgs.

The integer feature switch parameters are defined as a sequence of `FSBoundedParam[Int]` objects. These parameters control the result size, batch size, and budget in milliseconds for fetching candidate sources and recent following predicates.

The double feature switch parameters are defined as a sequence of `FSBoundedParam[Double]` objects. These parameters control the weights for various candidate sources, such as phone book, email book, strong tie prediction, triangular loops, user-user graph, new following expansion, similar user, recent engagement, repeated profile visits, real graph oon, pop country, pop geohash, pop country backfill, PPMI locale follow, top organic follows accounts, and crowd search account.

Overall, this configuration file allows for fine-grained control over the content recommender flow in the Twitter application by enabling or disabling certain candidate sources and predicates, and adjusting their weights and budgets. It can be used in conjunction with other files and modules to create a robust and effective content recommendation system for Twitter users. 

Example usage:

```scala
val config = new ContentRecommenderFlowFSConfig()
val includeSocialBased = config.booleanFSParams.contains(ContentRecommenderParams.IncludeSocialBasedCandidateSource)
val resultSize = config.intFSParams.find(_.name == ContentRecommenderParams.ResultSizeParam.name).map(_.value).getOrElse(10)
val userUserGraphWeight = config.doubleFSParams.find(_.name == ContentRecommenderFlowCandidateSourceWeightsParams.UserUserGraphSourceWeight.name).map(_.value).getOrElse(0.5)
``` 

In this example, we create a new instance of the `ContentRecommenderFlowFSConfig` class and use it to retrieve the boolean feature switch parameter for including social-based candidate sources, the integer feature switch parameter for the result size, and the double feature switch parameter for the user-user graph source weight. These values can then be used in other parts of the application to customize the content recommender flow.
## Questions: 
 1. What is the purpose of this code and what does it do?
- This code defines a configuration class for feature switches in the Content Recommender Flow of the Twitter Follow Recommendations project. It specifies boolean, integer, and double parameters for various candidate sources and weights used in the flow.

2. What other classes or files does this code interact with?
- This code imports classes from `com.twitter.follow_recommendations.configapi.common` and `com.twitter.timelines.configapi`, and likely interacts with other classes in the `com.twitter.follow_recommendations.flows.content_recommender_flow` package.

3. What is the significance of the `@Singleton` and `@Inject` annotations in this code?
- The `@Singleton` annotation indicates that only one instance of this class should be created and shared across the application. The `@Inject` annotation indicates that this class should be instantiated and managed by a dependency injection framework.