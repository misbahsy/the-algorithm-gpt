[View code on GitHub](https://github.com/misbahsy/the-algorithm/follow-recommendations-service/common/src/main/scala/com/twitter/follow_recommendations/common/models/TrackingToken.scala)

The `TrackingToken` class is used for attribution per target-candidate pair in the Twitter Follow Recommendations project. It contains four fields: `sessionId`, `displayLocation`, `controllerData`, and `algorithmId`. The `sessionId` field is the trace-id of the Finagle request. The `displayLocation` field is an optional `DisplayLocation` object that represents the location where the recommendation was displayed. The `controllerData` field is an optional `ControllerData` object that contains binary attributes of the recommendation. The `algorithmId` field is an optional integer that identifies a candidate source and is maintained for backwards compatibility.

The `TrackingToken` class has two methods: `toThrift` and `toOfflineThrift`. Both methods convert the `TrackingToken` object to a Thrift object, but `toThrift` returns a `t.TrackingToken` object and `toOfflineThrift` returns an `offline.TrackingToken` object. The `t.TrackingToken` object is used for online tracking, while the `offline.TrackingToken` object is used for offline tracking.

The `TrackingToken` object can be serialized and deserialized using the `serialize` and `deserialize` methods. The `serialize` method takes a `TrackingToken` object and returns a Base64-encoded string representation of the Thrift object. The `deserialize` method takes a Base64-encoded string and returns a `TrackingToken` object.

The `fromThrift` method is a helper method that takes a `t.TrackingToken` object and returns a `TrackingToken` object. This method is used by the `deserialize` method to convert the Thrift object back to a `TrackingToken` object.

The `HasTrackingToken` trait is a marker trait that indicates that a class has a `trackingToken` field of type `Option[TrackingToken]`. This trait is used to enforce the presence of a `trackingToken` field in certain classes.

Overall, the `TrackingToken` class and its associated methods are used to track recommendations in the Twitter Follow Recommendations project. The class contains information about the recommendation, such as the location where it was displayed and the binary attributes of the recommendation. The class can be serialized and deserialized for online and offline tracking purposes.
## Questions: 
 1. What is the purpose of the `TrackingToken` class?
- The `TrackingToken` class is used for attribution per target-candidate pair, and contains a trace-id of the finagle request, binary attributes of the recommendation, and an id for identifying a candidate source.

2. What is the difference between the `toThrift` and `toOfflineThrift` methods in the `TrackingToken` class?
- The `toThrift` method returns a `t.TrackingToken` object, while the `toOfflineThrift` method returns an `offline.TrackingToken` object.

3. What is the purpose of the `HasTrackingToken` trait?
- The `HasTrackingToken` trait defines a method `trackingToken` that returns an optional `TrackingToken` object, indicating that a class implementing this trait has a tracking token associated with it.