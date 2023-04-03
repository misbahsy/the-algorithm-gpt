[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/java/com/twitter/search/common/schema/earlybird/EarlybirdSchemaBuilder.java)

The EarlybirdSchemaBuilder class is used to build a ThriftSchema for the Earlybird project. The class extends the SchemaBuilder class and provides additional functionality specific to the Earlybird project. 

The constructor takes in three parameters: an instance of FieldNameToIdMapping, an instance of EarlybirdCluster, and an instance of TokenStreamSerializer.Version. The FieldNameToIdMapping class maps field names to field IDs, while the EarlybirdCluster class represents the cluster that the schema is being built for. The TokenStreamSerializer.Version class represents the version of the token stream serializer being used.

The class provides several methods for configuring the schema. The withOutOfOrderEnabledForField method configures a specified field to be out-of-order. This causes Earlybird to use the skip list posting format in the realtime cluster. The withTweetSpecificNormalization method turns on tweet-specific normalizations for a specified field. This includes the HashtagMentionPunctuationSplitter and NormalizedTokenFilter token processors. The withPhotoUrlFacetField method adds a twitter photo facet field to the schema.

The shouldIncludeField method is used to determine whether a given field should be included or dropped. It returns true if the field is a valid field in the Earlybird cluster and false otherwise.

Overall, the EarlybirdSchemaBuilder class is an important part of the Earlybird project as it provides functionality for building a ThriftSchema that is specific to the Earlybird cluster. It allows for the configuration of fields to be out-of-order, tweet-specific normalizations, and twitter photo facet fields.
## Questions: 
 1. What is the purpose of this code?
- This code is used to build a ThriftSchema for the Earlybird project from Twitter.

2. What are the parameters of the constructor for EarlybirdSchemaBuilder?
- The constructor takes in an instance of FieldNameToIdMapping, an instance of EarlybirdCluster, and a version of TokenStreamSerializer.

3. What does the method withTweetSpecificNormalization do?
- The method turns on tweet specific normalizations for a specified field, which includes splitting mentions and hashtags into tokens and stripping out certain characters from the tokens.