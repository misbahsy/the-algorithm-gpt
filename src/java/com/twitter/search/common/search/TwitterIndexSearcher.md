[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/java/com/twitter/search/common/search/TwitterIndexSearcher.java)

The TwitterIndexSearcher class is an extension of the Lucene IndexSearcher class that provides additional functionality for early termination of search results. The class overrides the search() method of the IndexSearcher class to provide early termination functionality when a TwitterEarlyTerminationCollector is passed in as a collector. If a stock Lucene collector is passed in, the search() method behaves the same as the stock IndexSearcher. 

The class provides two additional methods, getNumericDocValues() and collectionStatistics(), that return NumericDocValues and CollectionStatistics objects respectively. The getNumericDocValues() method returns the NumericDocValues for a given field, or null if no NumericDocValues were indexed for the field. The collectionStatistics() method returns the CollectionStatistics for a given field, or null if the field is not found in the index. 

The class also provides a termStatistics() method that returns a TermStatistics object for a given term, doc frequency, and total term frequency. The method ensures that the doc frequency and total term frequency are at least 1, as Lucene 8.0.0 expects them to be. 

Overall, the TwitterIndexSearcher class provides additional functionality for early termination of search results and retrieval of NumericDocValues and CollectionStatistics objects. It can be used in conjunction with the TwitterEarlyTerminationCollector to provide early termination of search results in the larger project. 

Example usage of the getNumericDocValues() method:

```
TwitterIndexSearcher searcher = new TwitterIndexSearcher(reader);
NumericDocValues values = searcher.getNumericDocValues("field_name");
```

Example usage of the collectionStatistics() method:

```
TwitterIndexSearcher searcher = new TwitterIndexSearcher(reader);
CollectionStatistics stats = searcher.collectionStatistics("field_name");
```

Example usage of the termStatistics() method:

```
Term term = new Term("field_name", "term_value");
int docFreq = 10;
long totalTermFreq = 20;
TermStatistics stats = TwitterIndexSearcher.termStats(term, docFreq, totalTermFreq);
```
## Questions: 
 1. What is the purpose of the TwitterEarlyTerminationCollector and how does this class work with it?
- The TwitterIndexSearcher class works with the TwitterEarlyTerminationCollector to perform early termination without relying on CollectionTerminatedException. If a TwitterEarlyTerminationCollector is passed in, the search() method in TwitterIndexSearcher performs Twitter style early termination.

2. What is the purpose of the getNumericDocValues() method?
- The getNumericDocValues() method returns NumericDocValues for a given field, or null if no NumericDocValues were indexed for that field. The returned instance should only be used by a single thread.

3. Why does the collectionStatistics() method cap the values of docsWithField, sumTotalTermFreq, and sumDocFreq?
- The collectionStatistics() method caps the values of docsWithField, sumTotalTermFreq, and sumDocFreq to ensure that the CollectionStatistics instance produced has all fields set to at least 1. This is necessary because Lucene 8.0.0 expects all int fields in CollectionStatistics instances to be strictly greater than 0, and Lucene itself produces null CollectionStatistics instances in a few places.