[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/java/com/twitter/search/common/query/MappableField.java)

The `MappableField` class is a part of the Twitter search project and is used to map fields declared in the class to fields internally without exposing their schemas to other services. This is useful for setting boosts for URL-like fields in Earlybird without direct knowledge of the internal Earlybird field name. 

The class is an enumeration that contains two fields: `REFERRAL` and `URL`. The static block initializes an immutable map that maps each `MappableField` value to its lowercase string representation. This map is stored in the `MAPPABLE_FIELD_TO_NAME_MAP` variable. 

The class provides two methods for accessing the map. The `mappableFieldName` method takes an `MappableField` value as an argument and returns its corresponding lowercase string representation. The `getName` method returns the lowercase string representation of the current `MappableField` instance. 

This class can be used in the larger project to provide a level of abstraction between the fields declared in the code and the internal fields used by other services. For example, if a boost needs to be set for a URL-like field in Earlybird, the `MappableField.URL` value can be used instead of the actual internal field name. This allows for greater flexibility and easier maintenance of the code. 

Example usage:

```
MappableField field = MappableField.URL;
String fieldName = field.getName(); // returns "url"
String mappableFieldName = MappableField.mappableFieldName(field); // also returns "url"
```
## Questions: 
 1. What is the purpose of the MappableField enum?
   - The MappableField enum is used to map fields declared here to fields internally without exposing their schemas to other services.
   
2. What is the significance of the static block in the code?
   - The static block is used to initialize the MAPPABLE_FIELD_TO_NAME_MAP ImmutableMap with the lowercase string representation of each MappableField enum value.
   
3. What do the mappableFieldName and getName methods do?
   - The mappableFieldName method returns the name of a given MappableField enum value by looking it up in the MAPPABLE_FIELD_TO_NAME_MAP ImmutableMap. The getName method returns the name of the current MappableField enum value by calling the mappableFieldName method with 'this' as the argument.