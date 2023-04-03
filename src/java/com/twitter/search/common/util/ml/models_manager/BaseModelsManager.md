[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/java/com/twitter/search/common/util/ml/models_manager/BaseModelsManager.java)

The `BaseModelsManager` class is responsible for loading machine learning models from Hadoop Distributed File System (HDFS) and providing an interface for reloading them periodically. The class is abstract, and its subclasses must implement the `readModelFromDirectory` method, which reads a model instance from the directory file instance. The `BaseModelsManager` class has two ways of detecting the active models: `DirectorySupplier` and `ConfigSupplier`. The former uses all the subdirectories of a base path, while the latter gets the list from a configuration file. 

The `BaseModelsManager` class has a `loadedModels` map that stores the loaded models, and a `lastModifiedMsByModel` map that stores the last modified timestamp of each model. The `run` method is responsible for loading the available models, either from the config file or by listing the base directory. If a model is updated or added, the method reads the model instance from the directory file instance and stores it in the `loadedModels` map. If a model is no longer active, the method removes it from the `loadedModels` map. 

The `getModel` method retrieves a particular model from the `loadedModels` map. If the `shouldServeModels` flag is set to false, the method returns an empty `Optional`. The `cleanUpUnloadedModel` method cleans up any resources used by the model instance. This method is called after removing the model from the in-memory map. Sub-classes can provide custom overridden implementation as required.

The `BaseModelsManager` class has several metrics that can be used to monitor the performance of the model loading process. The `numModels` metric counts the number of loaded models, the `numErrors` metric counts the number of errors that occurred during the model loading process, and the `lastLoadedMs` metric stores the timestamp of the last loaded model. 

The `BaseModelsManager` class has two constructors. The first constructor takes the `activeModelsSupplier`, `shouldUnloadInactiveModels`, and `statsPrefix` parameters. The `activeModelsSupplier` parameter is a supplier that provides the active list of models. The `shouldUnloadInactiveModels` parameter determines whether models are unloaded immediately when they're removed from `activeModelsSupplier`. If false, old models stay in memory until the process is restarted. The `statsPrefix` parameter is a prefix used to name the metrics. The second constructor takes two additional parameters: `shouldServeModels` and `shouldLoadModels`. The `shouldServeModels` parameter is a supplier that determines whether the `getModel` method should return a model. The `shouldLoadModels` parameter is a supplier that determines whether the model loading process should be executed.

The `BaseModelsManager` class has a `scheduleAtFixedRate` method that schedules the loader to run periodically. The method takes the `period`, `timeUnit`, and `builderThreadName` parameters. The `period` parameter is the period between executions, the `timeUnit` parameter is the time unit of the period parameter, and the `builderThreadName` parameter is the name of the thread that executes the loader. 

The `DirectorySupplier` class is a nested class that implements the `Supplier` interface. It gets the active list of models from the subdirectories in a base directory. Each model is identified by the name of the subdirectory. The `ConfigSupplier` class is another nested class that implements the `Supplier` interface. It gets the active list of models by reading a YAML config file. The keys are the model names, and the values are dictionaries with a single entry for the path of the model in HDFS (without the HDFS name node prefix).
## Questions: 
 1. What is the purpose of this code?
- This code is a base class for loading machine learning models from HDFS and provides an interface for reloading them periodically.

2. What are the two possible ways of detecting the active models?
- The two possible ways are: using all the subdirectories of a base path (DirectorySupplier) or getting the list from a configuration file (ConfigSupplier).

3. What is the purpose of the shouldUnloadInactiveModels flag?
- This flag determines whether models are unloaded immediately when they're removed from activeModelsSupplier. If false, old models stay in memory until the process is restarted. This may be useful to safely change model configuration without restarting.