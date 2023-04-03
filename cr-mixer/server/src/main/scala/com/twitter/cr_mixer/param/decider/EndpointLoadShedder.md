[View code on GitHub](https://github.com/misbahsy/the-algorithm/cr-mixer/server/src/main/scala/com/twitter/cr_mixer/param/decider/EndpointLoadShedder.scala)

The `EndpointLoadShedder` class provides decider-controlled load shedding for a given product from a given endpoint. It takes in a `Decider` and a `StatsReceiver` as parameters and returns a `Future` of the type `T`. The `Decider` is used to determine whether to shed load or not, while the `StatsReceiver` is used to track the number of requests that are being shed.

The `apply` method takes in the endpoint name and product name as parameters and a `Future` that returns the result of the request. It checks if either per-product or top-level load shedding is enabled. If both are enabled at different percentages, load shedding will not be perfectly calculable due to salting of hash. If load shedding is enabled, it increments the counter for the corresponding key in the `StatsReceiver` and returns a `Future` that throws a `LoadSheddingException`. If load shedding is not enabled, it returns the result of the request.

The `LoadSheddingException` object is an exception that is thrown when load shedding is enabled for a request.

This class is used in the larger project to control the amount of load on a given endpoint for a given product. It is particularly useful during incidents when the load on the system is high and needs to be controlled. By defining keys for the endpoints/products that are most important in the `decider.yml` file, the load on those endpoints/products can be controlled during incidents. 

Example usage:

```scala
val endpointLoadShedder = EndpointLoadShedder(decider, statsReceiver)

val result = endpointLoadShedder("getTweetRecommendations", "Notifications") {
  // code to get tweet recommendations for notifications
}
```
## Questions: 
 1. What is the purpose of this code?
    
    This code provides deciders-controlled load shedding for a given Product from a given endpoint. It checks if either per-product or top-level load shedding is enabled and serves the request accordingly.

2. What is the significance of the `enable_loadshedding` key prefix?
    
    The `enable_loadshedding` key prefix is used to define decider keys for the endpoints/product we care most about in decider.yml, so that we can control them during incidents.

3. How does the load shedding work if both per-product and top-level load shedding are enabled at different percentages?
    
    If both per-product and top-level load shedding are enabled at different percentages, load shedding will not be perfectly calculable due to salting of hash (i.e. 25% load shed for Product x + 25% load shed for overall does not result in 50% load shed for x).