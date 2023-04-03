[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/scala/com/twitter/simclusters_v2/scalding/offline_job/adhoc/SimClustersTweetEmbeddingAdhocApp.scala)

The `SimClustersTweetEmbeddingAdhocApp` is an adhoc job for computing Tweet SimClusters embeddings. The output of this job includes two data sets: tweet -> top clusters (or Tweet Embedding), and cluster -> top tweets. These data sets are supposed to be the snapshot of the two index at the end of the dataRange you run. 

The purpose of this code is to provide a flexible way to experiment with different ideas for computing Tweet SimClusters embeddings. It is recommended to put at least 2 days in the `--date` parameter in order to make sure there is enough engagement data for tweets that have more engagements in the last 1+ days. 

There are several parameters to tune in the job, which are explained in the inline comments. The job reads user-tweet fav data and sets the weight to be a decayed value. They will be decayed to the `dateRange.end`. The job also filters out tweets that have less than X favs in the `dateRange`. 

The job constructs a user-simclusters matrix and multiplies the tweet -> user matrix with the user -> cluster matrix to get the tweet -> cluster matrix. The tweet -> top clusters are obtained by taking the top K in each row, and the cluster -> top tweets are obtained by taking the top K in each column. 

The job saves the data sets and also outputs to some TSV files for eyeballing the results. 

To run the job, the following command can be used:

```
scalding remote run \
--target src/scala/com/twitter/simclusters_v2/scalding/offline_job/adhoc:tweet_embedding-adhoc \
--user recos-platform \
--reducers 1000 \
--main-class com.twitter.simclusters_v2.scalding.offline_job.adhoc.SimClustersTweetEmbeddingAdhocApp -- \
--date 2021-01-27 2021-01-28 \
--score_type logFav \
--output_dir /user/recos-platform/adhoc/tweet_embedding_01_27_28_unnormalized_t9
```
## Questions: 
 1. What is the purpose of this code and what are the expected outputs?
- The purpose of this code is to compute Tweet SimClusters embeddings and output two datasets: tweet -> top clusters (or Tweet Embedding), and cluster -> top tweets. These datasets are supposed to be the snapshot of the two index at the end of the dataRange you run.
- The expected outputs are saved in two subfolders: tweet_top_k_clusters and cluster_top_k_tweets.

2. What are the parameters that can be tuned in this job and what do they do?
- There are several parameters that can be tuned in this job, including:
  - score_type: what interestedIn score to use. logFav is what is used in production.
  - run_normalized: whether to use normalized score in the cluster -> top tweets. Currently, this is not done in production and should not be turned on unless you know what you are doing.
  - tweet_fav_threshold: filter out tweets that have less than X favs in the dateRange.
- These parameters are explained in the inline comments.

3. How can this job be run and what are the required arguments?
- This job can be run using the `scalding remote run` command.
- The required arguments include:
  - target: the path to the file containing the main class to run.
  - user: the user to run the job as.
  - reducers: the number of reducers to use.
  - date: the date range to run the job on.
  - score_type: (optional) what interestedIn score to use.
  - output_dir: the directory to save the output datasets in.