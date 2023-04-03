[View code on GitHub](https://github.com/misbahsy/the-algorithm/product-mixer/core/src/main/scala/com/twitter/product_mixer/core/model/marshalling/response/urt/promoted/AdMetadataContainer.scala)

The `AdMetadataContainer` case class is a data model used for marshalling responses related to promoted content in the Twitter product mixer. It contains several optional fields that provide metadata about a promoted ad, including information about the sponsoring organization, the type of sponsorship, and any associated disclaimers.

One notable field is `skAdNetworkDataList`, which is an optional sequence of `SkAdNetworkData` objects. This field is used to store data related to the SKAdNetwork framework, which is used for measuring the effectiveness of ad campaigns on iOS devices. The `unifiedCardOverride` field is another optional field that can be used to override the default card used to display promoted content.

Overall, this case class is used to represent metadata about promoted content in the Twitter product mixer. It can be used in conjunction with other classes and methods to generate responses that include information about promoted ads, which can be used to inform ad targeting and optimization strategies. 

Example usage:

```scala
val adMetadata = AdMetadataContainer(
  removePromotedAttributionForPreroll = Some(true),
  sponsorshipCandidate = Some("Acme Corp."),
  sponsorshipOrganization = Some("Acme Corp."),
  sponsorshipOrganizationWebsite = Some("https://www.acme.com"),
  sponsorshipType = Some(SponsorshipType.PROMOTED),
  disclaimerType = Some(DisclaimerType.SPONSORED),
  skAdNetworkDataList = Some(Seq(SkAdNetworkData(
    version = "2.2",
    network = "abcde12345.skadnetwork",
    campaignId = "123456789",
    itunesItemId = "987654321"
  ))),
  unifiedCardOverride = Some("custom_card")
)

// Use the adMetadata object to generate a response
```
## Questions: 
 1. What is the purpose of the AdMetadataContainer case class?
- The AdMetadataContainer case class is used for marshalling response data related to promoted ads, including information about sponsorship, disclaimers, and SKAdNetwork data.

2. What are the possible values for the sponsorshipType and disclaimerType options?
- The sponsorshipType option can have values of either "SPONSORED" or "PROMOTED", while the disclaimerType option can have values of "SPONSORED_DISCLAIMER" or "PROMOTED_DISCLAIMER".
 
3. What is the unifiedCardOverride option used for?
- The unifiedCardOverride option is used to override the default card for a promoted tweet with a custom card.