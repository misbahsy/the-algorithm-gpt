[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/scala/com/twitter/simclusters_v2/summingbird/stores/UserInterestedInReadableStore.scala)

The `UserInterestedInReadableStore` object provides methods for accessing and reading data from various Manhattan key-value stores related to user interests in clusters. The object contains several maps that map different model versions to their corresponding data sets. The `defaultStoreWithMtls` method returns a `ReadableStore` of `ClustersUserIsInterestedIn` objects, which represent the clusters that a user is interested in. The method takes a `ManhattanKVClientMtlsParams` object and a model version string as input and returns a `ReadableStore` that can be used to read data from the corresponding data set. 

The `defaultSimClustersEmbeddingStoreWithMtls` method returns a `ReadableStore` of `SimClustersEmbedding` objects, which represent the embeddings of the clusters that a user is interested in. The method takes a `ManhattanKVClientMtlsParams` object, an `EmbeddingType` object, and a `ModelVersion` object as input and returns a `ReadableStore` that can be used to read data from the corresponding data set. The `toSimClustersEmbedding` method is used to convert `ClustersUserIsInterestedIn` objects to `SimClustersEmbedding` objects.

Overall, this object provides a convenient way to access and read data related to user interests in clusters from various Manhattan key-value stores. It can be used in conjunction with other parts of the larger project to analyze and model user behavior. 

Example usage:

```
val mtlsParams = ManhattanKVClientMtlsParams(...)
val userInterestedInStore = UserInterestedInReadableStore.defaultStoreWithMtls(mtlsParams)
val userInterestedIn = userInterestedInStore.get(userId)
val embeddingStore = UserInterestedInReadableStore.defaultSimClustersEmbeddingStoreWithMtls(mtlsParams, EmbeddingType.FavBasedUserInterestedIn, ModelVersions.Model20M145KUpdated)
val embedding = embeddingStore.get(simClustersEmbeddingId)
```
## Questions: 
 1. What is the purpose of this code and what problem does it solve?
- This code provides various methods to access and retrieve user interested in data from different datasets stored in ManhattanKV. It also includes a method to convert the retrieved data into a SimClustersEmbedding object.

2. What are the different datasets available and how are they mapped to model versions?
- The code includes several maps that map different model versions to their corresponding datasets. These maps include modelVersionToDatasetMap, modelVersionToDenserDatasetMap, modelVersionToIIAPEDatasetMap, modelVersionToIIKFLiteDatasetMap, and modelVersionToNextInterestedInDatasetMap.

3. What is the purpose of the toSimClustersEmbedding method and how is it used?
- The toSimClustersEmbedding method is used to convert ClustersUserIsInterestedIn thrift struct data into a SimClustersEmbedding object. It takes in the record data, embedding type, and an optional maxClusterSize parameter and returns a SimClustersEmbedding object. This method is used in several other methods to convert the retrieved data into a usable format.