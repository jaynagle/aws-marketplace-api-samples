### Start a new RestrictDeliveryOptions ChangeSet on Catalog API
This sample starts a `RestrictDeliveryOptions` ChangeSet on an AmiProduct entity using `StartChangeSet` operation in AWS Marketplace Catalog API. To run the sample, set `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_SESSION_TOKEN`, and `AWS_REGION` parameters in terminal session.

Details of available request parameters can be found [here](../../../../change-types/restrict-delivery-options).

**Example 1 (with intermediate variables)**
```commandline
# Set details JSON
DETAILS_JSON_AS_STRING=$(echo '
{
  "DeliveryOptionIds": [
    "00000000-0000-0000-0000-000000000000"
  ]
}' | jq "tostring")

# Run AWS CLI command
aws marketplace-catalog start-change-set \
  --catalog "AWSMarketplace" \
  --change-set '[
      {
        "ChangeType": "RestrictDeliveryOptions",
        "Entity": {
          "Identifier": "10000000-0000-0000-0000-000000000000",
          "Type": "AmiProduct@1.0"
        },
        "Details": '"${DETAILS_JSON_AS_STRING}"'
      }
    ]'
```

**Example 2 (in-line invocation)**

```commandline
aws marketplace-catalog start-change-set \
--catalog "AWSMarketplace" \
--change-set '[
    {
      "ChangeType": "RestrictDeliveryOptions",
      "Entity": {
          "Identifier": "10000000-0000-0000-0000-000000000000",
          "Type": "AmiProduct@1.0"
      },
      "Details": "{\"DeliveryOptionIds\": [\"00000000-0000-0000-0000-000000000000\"]}"
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