[View code on GitHub](https://github.com/misbahsy/the-algorithm/timelines/data_processing/ad_hoc/earlybird_ranking/earlybird_ranking/training_data_generation/EarlybirdTrainingDataJob.scala)

This code generates data for training an Earlybird-friendly model. The Earlybird model is a machine learning model used by Twitter to predict user engagement with tweets. The purpose of this code is to produce a single "global" engagement and sample data accordingly. It also converts features from Earlybird to their original Earlybird feature names so they can be used as is in EB. 

The code takes in four arguments: 
- `input`: path to raw Recap training data (all labels)
- `output`: path to write sampled Earlybird-friendly training data
- `seed`: (optional) for random number generator (in sampling)
- `parallelism`: (default: 1) number of days to generate data for in parallel [splits long date range into single days]

The `GenerateEarlybirdTrainingData` trait is used to generate the training data. It extends the `OfflineExecution` trait and overrides the `executionFromParams` method. The `isEligibleForEarlybirdScoring` method is used to filter out records that are not eligible for Earlybird scoring. 

The `runDateRangeWithParallelism` method is used to split the date range into single days and generate data for each day in parallel. The `HourlySuffixFeatureSource` is used to read the data from the input path. The `EarlybirdExampleSampler` is used to weight and sample the data. The `EarlybirdFeatureRenamer` is used to convert the features from Earlybird to their original Earlybird feature names. The data is then shuffled row-wise to get rid of clustered replies and written to the output path. 

There are two objects that extend the `GenerateEarlybirdTrainingData` trait: `EarlybirdTrainingDataAdHocJob` and `EarlybirdTrainingDataProdJob`. These objects are used to generate the training data for ad-hoc and production jobs respectively. 

Example usage: 

```
val args = Args(
  Seq(
    "--input", "/path/to/raw/training/data",
    "--output", "/path/to/output/training/data",
    "--seed", "123",
    "--parallelism", "4"
  )
)

EarlybirdTrainingDataAdHocJob.executionFromParams(args)(DateRange.yesterday)
```
## Questions: 
 1. What is the purpose of this code?
- This code generates data for training an Earlybird-friendly model by producing a single "global" engagement and sampling data accordingly. It also converts features from Earlybird to their original Earlybird feature names so they can be used as is in EB.

2. What are the input and output paths for this code?
- The input path is specified by the `--input` argument, which is the path to raw Recap training data (all labels). The output path is specified by the `--output` argument, which is the path to write sampled Earlybird-friendly training data.

3. What is the significance of the `isEligibleForEarlybirdScoring` method?
- The `isEligibleForEarlybirdScoring` method checks whether a given record is eligible for Earlybird scoring based on its Earlybird score. If the score is less than or equal to 100.0, the record is considered eligible. This logic is explained further in TQ-9678.