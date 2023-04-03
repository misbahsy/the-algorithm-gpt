[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/java/com/twitter/search/common/query/FieldRankHitInfo.java)

The `FieldRankHitInfo` class is used in the Twitter search algorithm to collect information about hits that occur during a search query. When a hit occurs on a part of the query tree, an instance of this class is passed to the `HitAttributeCollector` for collection. 

This class carries information about the hit, including the field that matched (recorded as a field ID), the query node that matched (recorded as a query node rank), and the ID of the last document that matched the query. Each `IdentifiableQuery` should be associated with one `FieldRankHitInfo`, which is passed to a `HitAttributeCollector` when a hit occurs.

The `FieldRankHitInfo` class has three instance variables: `fieldId`, `rank`, and `docId`. The `fieldId` and `rank` variables are set in the constructor and are immutable. The `docId` variable is initially set to `-1` (which is defined as `UNSET_DOC_ID`) and can be set to a different value using the `setDocId` method. The `resetDocId` method can be used to reset the `docId` to its initial value of `-1`.

This class is a simple data container that is used to pass information about a hit to the `HitAttributeCollector`. It does not perform any complex operations or calculations. An example of how this class might be used in the larger Twitter search algorithm is as follows:

```
FieldRankHitInfo hitInfo = new FieldRankHitInfo(fieldId, rank);
hitInfo.setDocId(docId);
hitAttributeCollector.collect(hitInfo);
```

In this example, a new `FieldRankHitInfo` object is created with the `fieldId` and `rank` values. The `docId` value is then set using the `setDocId` method. Finally, the `hitInfo` object is passed to the `collect` method of the `HitAttributeCollector`. This allows the `HitAttributeCollector` to collect information about the hit and use it to rank the search results.
## Questions: 
 1. What is the purpose of this class and how is it used in the larger project?
   - This class is used to store information about a query hit and is passed to a HitAttributeCollector for collection. It records the field that matched, the query node that matched, and the ID of the last doc that matched the query.
2. What is the significance of the UNSET_DOC_ID constant and how is it used?
   - The UNSET_DOC_ID constant is set to -1 and is used to indicate that the doc ID has not been set yet. It is used in the `docId` field and the `resetDocId()` method.
3. What is the relationship between IdentifiableQuery and FieldRankHitInfo?
   - Each IdentifiableQuery should be associated with one FieldRankHitInfo, which is passed to a HitAttributeCollector when a hit occurs. FieldRankHitInfo stores information about the hit, while IdentifiableQuery is responsible for identifying the query that produced the hit.