[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/java/com/twitter/search/common/schema/base/FieldWeightDefault.java)

The `FieldWeightDefault` class is used to record whether a field is enabled for search by default and its default weight. The class is mutable and has two fields: `enabled` and `weight`. The `enabled` field is a boolean that indicates whether the field is enabled for search by default, while the `weight` field is a float that represents the default weight of the field. 

The class has a constructor that takes two arguments: `enabled` and `weight`. It also has a static method `fromSignedWeight` that takes a float value and returns a new `FieldWeightDefault` instance. The `fromSignedWeight` method is used to create a new instance of `FieldWeightDefault` from a signed weight value. If the signed value is greater than or equal to zero, the `enabled` field is set to `true`, otherwise it is set to `false`. The `weight` field is set to the absolute value of the signed value.

The class also has three static methods: `getOnlyEnabled`, `overrideFieldWeightMap`, and `fromSignedWeightMap`. The `getOnlyEnabled` method takes a map of field names to `FieldWeightDefault` instances and returns an immutable map of only the enabled fields and their default weights. The `overrideFieldWeightMap` method takes a base map of field names to `FieldWeightDefault` instances and an overlay map of field names to double values. It returns an immutable map that is an overlay of the base map and the overlay map. The `fromSignedWeightMap` method takes a map of field names to signed weight values and returns an immutable map of field names to `FieldWeightDefault` instances.

The `FieldWeightDefault` class is used in the larger project to manage the default weights of fields that are enabled for search. It provides methods to create, modify, and retrieve maps of field names to default weights. For example, the `getOnlyEnabled` method can be used to retrieve a map of only the enabled fields and their default weights, which can be used to construct a query for searching. The `overrideFieldWeightMap` method can be used to modify the default weights of fields in a base map, which can be useful for customizing search results. The `fromSignedWeightMap` method can be used to create a map of field names to `FieldWeightDefault` instances from a map of field names to signed weight values. 

Example usage:

```
// create a new FieldWeightDefault instance
FieldWeightDefault fieldWeightDefault = new FieldWeightDefault(true, 1.0f);

// create a map of field names to FieldWeightDefault instances
Map<String, FieldWeightDefault> fieldWeightMap = new HashMap<>();
fieldWeightMap.put("field1", new FieldWeightDefault(true, 1.0f));
fieldWeightMap.put("field2", new FieldWeightDefault(false, 0.5f));

// get a map of only the enabled fields and their default weights
ImmutableMap<String, Float> enabledFields = FieldWeightDefault.getOnlyEnabled(fieldWeightMap);

// override the default weights of fields in a base map
Map<String, Double> overrideMap = new HashMap<>();
overrideMap.put("field1", 2.0);
ImmutableMap<String, FieldWeightDefault> overriddenMap = FieldWeightDefault.overrideFieldWeightMap(fieldWeightMap, overrideMap);

// create a map of field names to FieldWeightDefault instances from a map of field names to signed weight values
Map<String, Double> signedWeightMap = new HashMap<>();
signedWeightMap.put("field1", 1.0);
signedWeightMap.put("field2", -0.5);
ImmutableMap<String, FieldWeightDefault> fieldWeightDefaultMap = FieldWeightDefault.fromSignedWeightMap(signedWeightMap);
```
## Questions: 
 1. What is the purpose of the `FieldWeightDefault` class?
- The `FieldWeightDefault` class records whether a field's enabled for search by default and its default weight.

2. What is the difference between `getOnlyEnabled` and `overrideFieldWeightMap` methods?
- `getOnlyEnabled` returns an immutable map from field name to default field weights for only enabled fields, while `overrideFieldWeightMap` overlays the base field-weight map with the given one.

3. What is the purpose of the `fromSignedWeightMap` method?
- The `fromSignedWeightMap` method creates a field-to-`FieldWeightDefault` map from the given field-to-weight map, where negative weight means the field is not enabled for search by default, but if it is, the absolute value of the weight shall be used.