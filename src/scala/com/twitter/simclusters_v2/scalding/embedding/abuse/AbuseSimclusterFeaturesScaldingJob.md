[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/scala/com/twitter/simclusters_v2/scalding/embedding/abuse/AbuseSimclusterFeaturesScaldingJob.scala)

The `AbuseSimclusterFeaturesScaldingJob` file is part of a larger project called The Algorithm from Twitter. The purpose of this file is to create single-side features used to predict abuse reports in search. The features are put into Manhattan and are available in the feature store. The job takes in a normalized sparse matrix of user interests, an unhealthy graph, and a healthy graph. It then builds a dataset of key-value pairs where the key is a user ID and the value is a `SingleSideUserScores` object. The `SingleSideUserScores` object contains four scores: `consumerHealthyScore`, `consumerUnhealthyScore`, `authorUnhealthyScore`, and `authorHealthyScore`. These scores are calculated using the `buildSearchAbuseScores` function, which takes in the normalized sparse matrix and the unhealthy and healthy graphs. The `buildSearchAbuseScores` function calculates the scores for each user by comparing their interactions with unhealthy and healthy content. The scores are then paired and written to the output path.

The `SearchAbuseSimclusterFeaturesScaldingJob` object is a scheduled execution app that runs the `AbuseSimclusterFeaturesScaldingJob` job on a weekly basis. It first gets the normalized sparse matrix of user interests and the unhealthy and healthy graphs. It then calls the `buildKeyValDataSet` function to build the dataset of key-value pairs. Finally, it writes the dataset to the output path using the `writeDALVersionedKeyValExecution` function.

The `AdhocSearchAbuseSimclusterFeaturesScaldingJob` object is an adhoc execution app that can be used to test the logic of the `AbuseSimclusterFeaturesScaldingJob` job. It takes in a date range and an output path and writes the output of the job to a TSV file.

Example usage:
```
// Run the scheduled job
$ hadoop jar myjar.jar com.twitter.simclusters_v2.scalding.embedding.abuse.SearchAbuseSimclusterFeaturesScaldingJob --local

// Run the adhoc job
$ hadoop jar myjar.jar com.twitter.simclusters_v2.scalding.embedding.abuse.AdhocSearchAbuseSimclusterFeaturesScaldingJob --local --date 2021-02-01 2021-02-02 --outputPath output.tsv
```
## Questions: 
 1. What is the purpose of the `AbuseSimclusterFeaturesScaldingJob` object?
- The `AbuseSimclusterFeaturesScaldingJob` object contains a method `buildKeyValDataSet` that builds a dataset of single-side user scores used to predict abuse reports in search.

2. What is the purpose of the `SearchAbuseSimclusterFeaturesScaldingJob` object?
- The `SearchAbuseSimclusterFeaturesScaldingJob` object is a scheduled execution app that creates single-side features used to predict abuse reports in search and writes them to a DAL versioned key-value dataset.

3. What is the purpose of the `AdhocSearchAbuseSimclusterFeaturesScaldingJob` object?
- The `AdhocSearchAbuseSimclusterFeaturesScaldingJob` object is an adhoc execution app that converts the output of `SearchAbuseSimclusterFeaturesScaldingJob.buildDataset()` to a TSV file.