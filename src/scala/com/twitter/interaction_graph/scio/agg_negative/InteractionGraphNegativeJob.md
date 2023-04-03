[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/scala/com/twitter/interaction_graph/scio/agg_negative/InteractionGraphNegativeJob.scala)

The `InteractionGraphNegativeJob` object is a Scala class that provides functionality for generating negative edge features in a social graph. The class reads input datasets containing negative signals such as blocks, mutes, abuse reports, spam reports, and unfollows, and groups all features by (source, destination) pairs. It then extracts the top K negative edges for each source node and saves them to Google Cloud Storage (GCS) and BigQuery (BQ) for further analysis.

The `configurePipeline` method is the main entry point for the class. It takes a `ScioContext` and an `InteractionGraphNegativeOption` object as input parameters. The `ScioContext` is used to read input datasets and write output data to GCS and BQ. The `InteractionGraphNegativeOption` object contains configuration options such as the output path and the time interval for which negative edge features should be generated.

The method reads input datasets containing negative signals such as blocks, mutes, abuse reports, spam reports, and unfollows. It then groups all features by (source, destination) pairs and extracts the top K negative edges for each source node. The `maxDestinationIds` variable specifies the maximum number of destination nodes to consider for each source node. The `pqMonoid` variable is an instance of the `PriorityQueueMonoid` class from the `com.twitter.algebird.mutable` package. It is used to maintain a priority queue of edges sorted by the number of negative features.

The method then saves the negative edge features to GCS and BQ. The `negativeFeatures` variable contains the top K negative edges for each source node. It is saved to GCS using the `DAL.writeVersionedKeyVal` method from the `com.twitter.beam.io.dal.DAL` package. The `allEdgeFeatures` variable contains all edges with their associated features. It is saved to BQ using the `BigQueryIO.write` method from the `org.apache.beam.sdk.io.gcp.bigquery` package.

The `readSnapshot` method is a helper method that reads the most recent snapshot of a given dataset from DAL. It takes a `SnapshotDALDataset` object and a `ScioContext` as input parameters and returns an `SCollection` of the corresponding Thrift struct.

Overall, the `InteractionGraphNegativeJob` class provides functionality for generating negative edge features in a social graph. It reads input datasets containing negative signals such as blocks, mutes, abuse reports, spam reports, and unfollows, and groups all features by (source, destination) pairs. It then extracts the top K negative edges for each source node and saves them to GCS and BQ for further analysis.
## Questions: 
 1. What is the purpose of this code and what problem does it solve?
- This code is a ScioBeamJob that reads input datasets of negative interactions (blocks, mutes, abuse reports, spam reports, and unfollows) and generates negative edge labels for a social graph. The negative edge labels are saved to both GCS and BigQuery. The purpose of this code is to identify negative interactions in a social graph and use them to generate recommendations for improving user experience.

2. What external libraries and APIs does this code use?
- This code uses several external libraries and APIs, including Google BigQuery, Spotify Scio, Twitter Algebird, Twitter Beam, Twitter DAL, Twitter Scrooge, and Twitter Socialgraph.

3. What is the data flow of this code and how are the negative edge labels generated?
- The code reads input datasets of negative interactions and groups all features by (source, destination). It then applies a top-K algorithm to select the K edges with the most negative features for each source node. The selected edges are used to generate negative edge labels, which are saved to GCS and BigQuery.