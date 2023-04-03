[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/java/com/twitter/search/earlybird/common/EarlybirdRequestPreLogger.java)

The `EarlybirdRequestPreLogger` class is a utility class that provides a way to log requests made to the Earlybird service. The class is used to create instances of `EarlybirdRequestLogger`, which is responsible for logging the requests. 

The `EarlybirdRequestPreLogger` class has two static factory methods: `buildForRoot` and `buildForShard`. The `buildForRoot` method is used to create an instance of `EarlybirdRequestPreLogger` for the root node of the Earlybird service. The `buildForShard` method is used to create an instance of `EarlybirdRequestPreLogger` for a shard of the Earlybird service. 

Both factory methods take a `Decider` object as a parameter. The `Decider` object is used to determine whether or not a request should be logged. If the `Decider` object returns `true`, the request is logged. If it returns `false`, the request is not logged. 

The `buildForRoot` method creates an instance of `EarlybirdRequestLogger` using the `buildForRoot` method of the `EarlybirdRequestLogger` class. The `buildForRoot` method takes the name of the class (`EarlybirdRequestPreLogger.class.getName()`), the maximum latency threshold (which is set to `Integer.MAX_VALUE`), and the `Decider` object as parameters. The method then returns a new instance of `EarlybirdRequestPreLogger` using the `EarlybirdRequestLogger` instance it created. 

The `buildForShard` method creates an instance of `EarlybirdRequestLogger` using the `buildForShard` method of the `EarlybirdRequestLogger` class. The `buildForShard` method takes the name of the class (`EarlybirdRequestPreLogger.class.getName()`), the latency warning threshold, and the `Decider` object as parameters. The method then returns a new instance of `EarlybirdRequestPreLogger` using the `EarlybirdRequestLogger` instance it created. 

The `EarlybirdRequestPreLogger` class has a private constructor that takes an instance of `EarlybirdRequestLogger` as a parameter. This constructor is used to create instances of `EarlybirdRequestPreLogger` from the factory methods. 

The `EarlybirdRequestPreLogger` class has a single public method: `logRequest`. This method takes an instance of `EarlybirdRequest` as a parameter and logs the request using the `logRequest` method of the `EarlybirdRequestLogger` instance that was passed to the constructor. 

Overall, the `EarlybirdRequestPreLogger` class provides a simple way to log requests made to the Earlybird service. It is used in conjunction with the `EarlybirdRequestLogger` class to provide detailed logging information for the Earlybird service.
## Questions: 
 1. What is the purpose of the EarlybirdRequestPreLogger class?
    
    The EarlybirdRequestPreLogger class is used to log EarlybirdRequest objects with a specified logger.

2. What is the difference between the buildForRoot and buildForShard methods?
    
    The buildForRoot method creates a logger for the root node of the EarlybirdRequest tree, while the buildForShard method creates a logger for a specific shard of the tree.

3. What parameters are required to create an instance of EarlybirdRequestPreLogger?
    
    An instance of EarlybirdRequestPreLogger requires a Decider object and either an integer value for latencyWarnThreshold (for buildForShard) or Integer.MAX_VALUE (for buildForRoot).