[View code on GitHub](https://github.com/misbahsy/the-algorithm/product-mixer/shared-library/src/main/scala/com/twitter/product_mixer/shared_library/thrift_client/FinagleThriftClientBuilder.scala)

The `FinagleThriftClientBuilder` object provides methods to build Finagle Thrift clients for a given service. The `buildFinagleMethodPerEndpoint` method builds a Finagle Thrift client that is method per endpoint based. This method requires values for fields that should always be set in practice, such as request timeouts. The method is useful when multiple versions of a client are needed for different timeout settings. The method takes in several parameters, including `serviceIdentifier`, `clientId`, `dest`, `label`, `statsReceiver`, `idempotency`, `timeoutPerRequest`, and `timeoutTotal`. The `buildFinagleServicePerEndpoint` method builds a Finagle Thrift client that is service per endpoint based. This method takes in similar parameters as the `buildFinagleMethodPerEndpoint` method. 

Both methods return a Finagle Thrift client that can be used to make requests to the specified service. The returned client can be used to call methods on the service, with the method name being the name of the endpoint. The client can be used to make synchronous or asynchronous requests. 

The `FinagleThriftClientBuilder` object is part of a larger project called The Algorithm from Twitter. This project likely involves building a distributed system that requires communication between different services. The Finagle Thrift clients built using the `FinagleThriftClientBuilder` object can be used to facilitate this communication. By providing a less error-prone way to build Finagle Thrift clients, the `FinagleThriftClientBuilder` object can help ensure that the clients are built correctly and consistently across the project.
## Questions: 
 1. What is the purpose of the `FinagleThriftClientBuilder` object?
- The `FinagleThriftClientBuilder` object provides methods to build Finagle Thrift clients with specific configurations, such as timeouts and idempotency semantics.

2. What is the difference between `buildFinagleMethodPerEndpoint` and `buildFinagleServicePerEndpoint` methods?
- `buildFinagleMethodPerEndpoint` builds a Finagle Thrift client with a method per endpoint API, while `buildFinagleServicePerEndpoint` builds a Finagle Thrift client with a service per endpoint API. The former is less error-prone and preferred in most cases, while the latter is useful when multiple versions of a client are needed.

3. What is the purpose of the `Idempotency` sealed trait and its case classes?
- The `Idempotency` sealed trait and its case classes define the idempotency semantics of a Finagle Thrift client. `NonIdempotent` means that requests are not idempotent, while `Idempotent` means that requests are idempotent with a maximum extra load percent specified.