### Start a new UpdateInformation ChangeSet on Catalog API
This sample starts a ChangeSet on an AmiProduct entity using `StartChangeSet` operation in AWS Marketplace Catalog API. To run the sample, set `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_SESSION_TOKEN`, `AWS_REGION`, and `ENTITY_ID` parameters in terminal session.

Details of available request parameters can be found [here](../../../../change-types/update-information).

**Example 1 (with intermediate variables)**
```commandline
# Set details JSON
DETAILS_JSON_AS_STRING=$(echo '
{
  "ProductTitle": "Sample product",
  "ShortDescription": "Brief description",
  "LongDescription": "Detailed description",
  "Sku": "SKU-123",
  "LogoUrl": "https://s3.amazonaws.com/logos/sample.png",
  "VideoUrls": [
    "https://sample.amazonaws.com/awsmp-video-1",
    "https://sample.amazonaws.com/awsmp-video-2"
  ],
  "Highlights": [
    "Sample highlight"
  ],
  "AdditionalResources": [
    {
      "Text": [
        "Sample resource",
        "https://sample.amazonaws.com"
      ]
    }
  ],
  "SupportDescription": "Product support information",
  "Categories": [
    "Operating Systems"
  ],
  "SearchKeywords": [
    "Sample keyword"
  ]
}' | jq "tostring")

# Run AWS CLI command
aws marketplace-catalog start-change-set \
  --catalog "AWSMarketplace" \
  --change-set '[
      {
        "ChangeType": "UpdateInformation",
        "Entity": {
          "Identifier": "10000000-0000-0000-0000-000000000000",
          "Type": "AmiProduct@1.0"
        },
        "Details": '"${DETAILS_JSON_AS_STRING}"'
      }
    ]';
```

**Example 2 (in-line invocation)**

```commandline
aws marketplace-catalog start-change-set \
--catalog "AWSMarketplace" \
--change-set '[
    {
      "ChangeType": "UpdateInformation",
      "Entity": {
          "Identifier": "10000000-0000-0000-0000-000000000000",
          "Type": "AmiProduct@1.0"
      },
      "Details": "{\"ProductTitle\": \"Sample product\", \"ShortDescription\": \"Brief description\", \"LongDescription\": \"Detailed description\", \"Sku\": \"SKU-123\", \"LogoUrl\": \"https:\/\/s3.amazonaws.com\/logos\/sample.png\", \"VideoUrls\": [\"https:\/\/sample.amazonaws.com\/awsmp-video-1\", \"https:\/\/sample.amazonaws.com\/awsmp-video-2\"], \"Highlights\": [\"Sample highlight\"], \"AdditionalResources\": [{\"Text\": [\"Sample resource\", \"https:\/\/sample.amazonaws.com\"]}], \"SupportDescription\": \"Product support information\", \"Categories\": [\"Operating Systems\"], \"SearchKeywords\": [\"Sample keyword\"]}"
    }
  ]';
```


**Response Structure**
```json
{
    "ChangeSetId": "sampleChangeSetId",
    "ChangeSetArn": "arn:aws:aws-marketplace:us-east-1:123456789012:AWSMarketplace/ChangeSet/sampleChangeSetId"
}
```