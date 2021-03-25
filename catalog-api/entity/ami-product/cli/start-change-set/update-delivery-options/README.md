### Start a new UpdateDeliveryOptions ChangeSet on Catalog API
This sample starts a ChangeSet on an AmiProduct entity using `StartChangeSet` operation in AWS Marketplace Catalog API. To run the sample, set `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_SESSION_TOKEN`, `AWS_REGION`, and `ENTITY_ID` parameters in terminal session.

**Example 1 (with intermediate variables)**
```commandline
# Set details JSON
DETAILS_JSON_AS_STRING=$(echo '
{
  "Version": {
    "ReleaseNotes": "Updated release notes"
  },
  "DeliveryOptions": [
    {
      "Id": "00000000-0000-0000-0000-000000000000",
      "Details": {
        "AmiDeliveryOptionDetails": {
          "UsageInstructions": "Updated usage instructions",
          "RecommendedInstanceType": "m4.2xlarge",
          "AccessEndpointUrl": {
            "Port": 8080,
            "Protocol": "https",
            "RelativePath": "index.html"
          },
          "SecurityGroups": [
            {
              "IpProtocol": "tcp",
              "FromPort": 443,
              "ToPort": 443,
              "IpRanges": [
                "0.0.0.0/0"
              ]
            }
          ]
        }
      }
    }
  ]
}' | jq "tostring")

# Run AWS CLI command
aws marketplace-catalog start-change-set \
  --catalog "AWSMarketplace" \
  --change-set '[
      {
        "ChangeType": "UpdateDeliveryOptions",
        "Entity": {
          "Identifier": "10000000-0000-0000-0000-000000000000",
          "Type": "AmiProduct@1.0"
        },
        "Details": '"${DETAILS_JSON_AS_STRING}"'
      }
    ]';
```

**Example 2 (compact invocation)**

```commandline
aws marketplace-catalog start-change-set \
--catalog "AWSMarketplace" \
--change-set '[
    {
      "ChangeType": "UpdateDeliveryOptions",
      "Entity": {
          "Identifier": "10000000-0000-0000-0000-000000000000",
          "Type": "AmiProduct@1.0"
      },
      "Details": "{\"Version\": {\"ReleaseNotes\": \"Updated release notes\"}, \"DeliveryOptions\": [{\"Id\": \"00000000-0000-0000-0000-000000000000\", \"Details\": {\"AmiDeliveryOptionDetails\": {\"UsageInstructions\": \"Updated usage instructions\", \"RecommendedInstanceType\": \"m4.2xlarge\", \"AccessEndpointUrl\": {\"Port\": 8080, \"Protocol\": \"https\", \"RelativePath\": \"index.html\"}, \"SecurityGroups\": [{\"IpProtocol\": \"tcp\", \"FromPort\": 443, \"ToPort\": 443, \"IpRanges\": [\"0.0.0.0\/0\"]}]}}}]}"
    }
  ]';
```


**Response Structure**
```json
{
    "ChangeSetId": "...",
    "ChangeSetArn": "arn:aws:aws-marketplace:us-east-1:<AWS_ACCOUNT_ID>:AWSMarketplace/ChangeSet/<CHANGE_SET_ID>"
}
```