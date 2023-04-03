[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/java/com/twitter/search/common/util/ml/prediction_engine/ModelLoader.java)

The `ModelLoader` class is responsible for loading `LightweightLinearModel` objects from a directory and providing an interface for reloading them periodically. The models must support the same features, defined by a `FeatureContext`, and are identified by the name of the subdirectory. The required directory structure is `/path/to/base-directory/one-model/model.tsv`, where each subdirectory must contain a file named `model.tsv` in the format required by `LightweightLinearModel`.

The `ModelLoader` class exports four counters: `last_loaded`, which is the timestamp (in ms) when the last model was loaded; `num_models`, which is the number of models currently loaded; `num_loads`, which is the number of successful model loads; and `num_errors`, which is the number of errors that occurred while loading the models.

The `getModel` method returns an `Optional` containing the `LightweightLinearModel` object with the given name, if it exists.

The `run` method loads the models from the base directory. It doesn't load a model if its file has not been modified since the last time it was loaded. This method doesn't delete previously loaded models if their directories are not available.

The `forDirectory` method creates an instance that loads models from a directory (local or from HDFS), while the `forHdfsDirectory` method creates an instance that loads models from HDFS.

The `IS_MODEL_DIR` filter is used to check if a file is a valid model directory. It returns `true` if the file is a directory and contains a readable `model.tsv` file.

Overall, the `ModelLoader` class provides a convenient way to load and manage `LightweightLinearModel` objects from a directory, making it easier to use them in the larger project.
## Questions: 
 1. What is the purpose of the `ModelLoader` class?
- The `ModelLoader` class loads `LightweightLinearModel` objects from a directory and provides an interface for reloading them periodically.

2. What is the required directory structure for the models?
- The required directory structure is a base directory containing subdirectories, where each subdirectory contains a file named `model.tsv` in the format required by `LightweightLinearModel`.

3. What metrics are exported by the `ModelLoader` class?
- The `ModelLoader` class exports 4 counters: `last_loaded`, `num_models`, `num_loads`, and `num_errors`.