[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/java/com/twitter/search/earlybird/partition/HdfsUtil.java)

The HdfsUtil class provides utility methods for interacting with Hadoop Distributed File System (HDFS) in the context of the larger project, The Algorithm from Twitter. The class contains two methods, `getHdfsFileSystem()` and `segmentExistsOnHdfs()`, both of which take a `FileSystem` object as a parameter.

The `getHdfsFileSystem()` method returns a new instance of `FileSystem` using the default Hadoop configuration. This method is used to ensure that each thread has its own `FileSystem` instance, as the project uses HDFS from different threads and closes the `FileSystem` from them independently.

The `segmentExistsOnHdfs()` method checks if a given segment is present on HDFS. It takes a `FileSystem` object and a `SegmentInfo` object as parameters. The `SegmentInfo` object contains information about the segment, including the HDFS upload directory prefix. The method uses the `globStatus()` method of the `FileSystem` object to get the status of the files that match the given path. If the status is not null and the length of the array is greater than 0, it means that the segment exists on HDFS.

Here is an example of how the `segmentExistsOnHdfs()` method can be used in the larger project:

```
FileSystem fs = HdfsUtil.getHdfsFileSystem();
SegmentInfo segmentInfo = new SegmentInfo(syncInfo);
boolean segmentExists = HdfsUtil.segmentExistsOnHdfs(fs, segmentInfo);
if (segmentExists) {
  // do something
} else {
  // do something else
}
```

In this example, we first get a new instance of `FileSystem` using the `getHdfsFileSystem()` method. We then create a `SegmentInfo` object using the `syncInfo` parameter. Finally, we use the `segmentExistsOnHdfs()` method to check if the segment exists on HDFS. Depending on the result, we can perform different actions.
## Questions: 
 1. What is the purpose of this code?
- This code provides utility methods for working with HDFS (Hadoop Distributed File System) in the context of the Earlybird project from Twitter.

2. Why is a new FileSystem instance created for each thread?
- Since Earlybird uses HDFS from different threads and closes the FileSystem from them independently, creating a new instance for each thread ensures that each thread has its own FileSystem and avoids conflicts.

3. What does the `segmentExistsOnHdfs` method do?
- This method checks if a given segment is present on HDFS by using the HDFS FileSystem object and the HDFS upload directory prefix obtained from the segment's sync info. It returns a boolean value indicating whether the segment exists or not.