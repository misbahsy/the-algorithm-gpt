[View code on GitHub](https://github.com/misbahsy/the-algorithm/product-mixer/core/src/main/scala/com/twitter/product_mixer/core/quality_factor/QualityFactorConfig.scala)

The code defines two implementations of the QualityFactorConfig trait: LinearLatencyQualityFactorConfig and QueriesPerSecondBasedQualityFactorConfig. 

Quality factor is an abstract number that enables a feedback loop to control operation costs and ultimately maintain the operation success rate. Abstractly, if operations/calls are too expensive (such as high latencies), the quality factor should go down, which helps future calls to ease their demand/load (such as reducing request width); if ops/calls are fast, the quality factor should go up, so we can incur more load.

LinearLatencyQualityFactorConfig is a linear quality factor implementation, aimed to achieve and maintain a percentile latency target. It adjusts the quality factor based on the latency of requests. If a request has a latency less than or equal to the target latency, the quality factor is increased by delta. If a request has a latency greater than the target latency, the quality factor is decreased by delta times the target percentile divided by 100 minus the target percentile. The target percentile is the percentile where the target latency is aimed at. 

QueriesPerSecondBasedQualityFactorConfig provides component capacity state based on sampling component Queries Per Second (qps) at the local host level. It adjusts the quality factor based on the number of queries per second observed on the local host. If the observed qps is less than or equal to the max qps the underlying component can take, the quality factor is increased by delta. If the observed qps is greater than the max qps, the quality factor is decreased by delta. 

Both implementations of QualityFactorConfig specify the quality factor min and max bounds and default value, initial delay, and ignorable failures. The ignorable failures are specified as a partial function of Throwable that should be ignored when calculating the quality factor. The defaultIgnorableFailures partial function ignores any Cancelled requests and ClientFailure. 

Overall, these implementations of QualityFactorConfig provide a way to adjust the quality factor based on either the latency of requests or the number of queries per second observed on the local host. This can help control operation costs and maintain the operation success rate.
## Questions: 
 1. What is the purpose of the `QualityFactorConfig` trait and its sub-classes?
- The `QualityFactorConfig` trait and its sub-classes define the configuration for calculating and adjusting a quality factor, which is used to control operation costs and maintain operation success rate.

2. What is the difference between `LinearLatencyQualityFactorConfig` and `QueriesPerSecondBasedQualityFactorConfig`?
- `LinearLatencyQualityFactorConfig` is used to maintain a percentile latency target, where the quality factor is adjusted based on the latency of requests. `QueriesPerSecondBasedQualityFactorConfig` is used to maintain a maximum queries per second threshold, where the quality factor is adjusted based on the observed queries per second on the local host.

3. What is the purpose of the `ignorableFailures` field in `QualityFactorConfig` and how is it used?
- The `ignorableFailures` field is a partial function that specifies which types of `Throwable`s should be ignored when calculating the quality factor. It is used to prevent certain types of failures from affecting the quality factor calculation, such as cancelled requests and client failures.