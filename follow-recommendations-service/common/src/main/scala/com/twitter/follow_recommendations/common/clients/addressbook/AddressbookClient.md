[View code on GitHub](https://github.com/misbahsy/the-algorithm/follow-recommendations-service/common/src/main/scala/com/twitter/follow_recommendations/common/clients/addressbook/AddressbookClient.scala)

The `AddressbookClient` class is a client for the Twitter Addressbook service. It provides methods for fetching user and contact data from the service. The class is implemented as a singleton and is injected with an instance of the `Addressbook2.MethodPerEndpoint` class, which is used to make requests to the Addressbook service.

The `getUsers` method is used to fetch user data from the Addressbook service. It takes a `userId` parameter, which is the ID of the user whose data is being fetched, and an `identifiers` parameter, which is a sequence of `RecordIdentifier` objects that identify the users whose data is being fetched. The `batchSize` parameter specifies the number of records to fetch in each batch, and the `edgeType` parameter specifies the type of edge to fetch. The `fetcherOption` parameter is an optional parameter that can be used to specify a fetcher to use for fetching data from the Addressbook service. The `maxFetches` parameter specifies the maximum number of fetches to make, and the `queryOption` parameter is an optional parameter that can be used to specify query options for the fetch.

The `getHashedContacts` method is used to fetch contact data from the Addressbook service. It takes two parameters: `normalizeFn` and `extractField`. The `normalizeFn` parameter is a function that is used to normalize the contact data before it is hashed. The `extractField` parameter specifies which field to extract from the contact data (either "emails" or "phoneNumbers"). The other parameters are the same as those for the `getUsers` method.

The `getUsersFromManhattan` and `getContactsFromManhattan` methods are used to fetch data from the Manhattan cache. They take a `userId` parameter and a `fetcher` parameter, which is used to fetch data from the cache.

The `createQueryOption` method is a utility method that is used to create a `QueryOption` object based on the `edgeType` and `isPhone` parameters.

Overall, the `AddressbookClient` class provides a convenient way to fetch user and contact data from the Twitter Addressbook service. It can be used in a variety of contexts, such as recommendation systems or social network analysis.
## Questions: 
 1. What is the purpose of the `AddressbookClient` class?
- The `AddressbookClient` class is a singleton class that provides methods for fetching user and contact information from the Addressbook2 service, with options for fetching from a cache or directly from the service.

2. What is the purpose of the `getHashedContacts` method?
- The `getHashedContacts` method is used to fetch and hash contact information (either emails or phone numbers) from the Addressbook2 service, with options for fetching from a cache or directly from the service.

3. What is the purpose of the `createQueryOption` method?
- The `createQueryOption` method is used to create a `QueryOption` object based on the edge type and whether the query is for phone numbers or emails. This object is used in the `getUsers` and `getHashedContacts` methods to specify query options for the Addressbook2 service.