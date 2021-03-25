### Start a new AddDeliveryOptions ChangeSet on Catalog API
This sample starts an `AddDeliveryOptions` ChangeSet on an AmiProduct entity using `StartChangeSet` operation in AWS Marketplace Catalog API. To run the sample, set `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_SESSION_TOKEN`, and `AWS_REGION` parameters in terminal session.

Details of available request parameters can be found [here](../../../../change-types/add-delivery-options). 

**Example 1 (with intermediate variables)**
```commandline
# Set details JSON
DETAILS_JSON_AS_STRING=$(echo '
{
  "Version": {
    "VersionTitle": "Sample title",
    "ReleaseNotes": "Sample release notes"
  },
  "DeliveryOptions": [
    {
      "Details": {
        "AmiDeliveryOptionDetails": {
          "AmiSource": {
            "AmiId": "ami-12345678",
            "AccessRoleArn": "arn:aws:iam::123456789012:role/sampleRole",
            "UserName": "Sample username",
            "OperatingSystemName": "Sample OS",
            "OperatingSystemVersion": "Sample OS Version"
          },
          "UsageInstructions": "Sample usage instructions",
          "RecommendedInstanceType": "m4.xlarge",
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
        "ChangeType": "AddDeliveryOptions",
        "Entity": {
          "Identifier": "00000000-0000-0000-0000-000000000000",
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
      "ChangeType": "AddDeliveryOptions",
      "Entity": {
          "Identifier": "00000000-0000-0000-0000-000000000000",
          "Type": "AmiProduct@1.0"
      },
      "Details": "{\"Version\": {\"VersionTitle\": \"Sample title\", \"ReleaseNotes\": \"Sample release notes\"}, \"DeliveryOptions\": [{\"Details\": {\"AmiDeliveryOptionDetails\": {\"AmiSource\": {\"AmiId\": \"ami-12345678\", \"AccessRoleArn\":\"arn:aws:iam::123456789012:role/sampleRole\", \"UserName\": \"Sample username\", \"OperatingSystemName\": \"Sample OS\", \"OperatingSystemVersion\": \"Sample OS Version\"}, \"UsageInstructions\": \"Sample usage instructions\", \"RecommendedInstanceType\": \"m4.xlarge\", \"SecurityGroups\": [{\"IpProtocol\": \"tcp\", \"FromPort\": 443, \"ToPort\": 443, \"IpRanges\": [\"0.0.0.0\/0\"]}]}}}]}"
    }
  ]'
```


**Response Structure**
```json
{
    "ChangeSetId": "sampleChangeSetId",
    "ChangeSetArn": "arn:aws:aws-marketplace:us-east-1:123456789012:AWSMarketplace/ChangeSet/sampleChangeSetId"
}
```