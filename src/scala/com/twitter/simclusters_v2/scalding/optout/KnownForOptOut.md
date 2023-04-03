[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/scala/com/twitter/simclusters_v2/scalding/optout/KnownForOptOut.scala)

The `KnownForOptOut` object provides a method to filter out opted-out clusters from a user's KnownFor dataset. The method takes three arguments: `knownForPipe`, `optedOutEntities`, and `clusterToEntities`. `knownForPipe` is a `TypedPipe` of `(UserId, ClustersUserIsKnownFor)` tuples, where `ClustersUserIsKnownFor` is a case class containing a `modelVersion` and a `Map[ClusterId, Map[SemanticCoreEntityId, Double]]`. `optedOutEntities` is a `TypedPipe` of `(UserId, Set[SemanticCoreEntityId])` tuples, where the `Set` contains the opted-out entities for each user. `clusterToEntities` is a `TypedPipe` of `(ClusterId, Seq[SemanticCoreEntityWithScore])` tuples, where `SemanticCoreEntityWithScore` is a case class containing a `coreEntityId` and a `score`.

The method first calls `SimClustersOptOutUtil.filterOptedOutClusters` to get the set of valid clusters for each user. This method takes the `userToClusters` argument, which is a `Map[UserId, Seq[ClusterId]]` containing the clusters for each user, and the `optedOutEntities` argument, which is the same as the `optedOutEntities` argument passed to the `filterOptedOutKnownFor` method. It also takes the `legibleClusters` argument, which is the same as the `clusterToEntities` argument passed to the `filterOptedOutKnownFor` method. The method returns a `Map[UserId, Set[ClusterId]]` containing the valid clusters for each user.

The `filterOptedOutKnownFor` method then performs a left join between `knownForPipe` and the valid clusters obtained from `SimClustersOptOutUtil.filterOptedOutClusters`. It then maps over the resulting `TypedPipe` to filter out the opted-out clusters for each user. Finally, it filters out any users whose KnownFor dataset is empty after filtering out the opted-out clusters.

The `KnownForOptOutDailyBatchJob` object is a scheduled Scalding job that runs daily. It reads the opted-out entities and cluster embeddings for the previous two days, and the KnownFor dataset for the previous ten days. It then calls the `filterOptedOutKnownFor` method to filter out opted-out clusters from the KnownFor dataset, and writes the resulting dataset to HDFS.

The `KnownForOptOutAdhocJob` object is an ad-hoc Scalding job that can be used for debugging. It reads the KnownFor dataset for the previous 30 days, the opted-out entities for the previous four days, and the cluster embeddings for the current day. It then calls the `filterOptedOutKnownFor` method to filter out opted-out clusters from the KnownFor dataset, and prints the differences between the original and filtered KnownFor datasets for each user.
## Questions: 
 1. What is the purpose of the `filterOptedOutKnownFor` function?
- The `filterOptedOutKnownFor` function creates opt-out compliant KnownFor datasets based on plain user -> KnownFor data and users' opt-out selections from YourTwitterData. It removes any cluster whose inferred entities were opted out by the user.

2. What is the purpose of the `KnownForOptOutDailyBatchJob` object?
- The `KnownForOptOutDailyBatchJob` object is a scheduled batch job that runs daily and creates opt-out compliant KnownFor datasets for the year 2020. It uses the `filterOptedOutKnownFor` function to filter out opted-out clusters from the plain KnownFor dataset.

3. What is the purpose of the `KnownForOptOutAdhocJob` object?
- The `KnownForOptOutAdhocJob` object is used for debugging purposes only. It runs a filtering job and prints the differences before and after the opt-out for a specific date range. It uses the `filterOptedOutKnownFor` function to filter out opted-out clusters from the plain KnownFor dataset.