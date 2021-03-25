### Describe a ChangeSet on Catalog API
This sample retrieves a ChangeSet using `DescribeChangeSet` operation in AWS Marketplace Catalog API. To run the sample, set `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_SESSION_TOKEN`, and `AWS_REGION` parameters in terminal session.

```commandline
# Run AWS CLI command
aws marketplace-catalog describe-change-set \
  --catalog "AWSMarketplace" \
  --change-set-id "<CHANGE_SET_ID>"
```

#### Response Structure
**Successfully completed ChangeSet**
```json
{
    "ChangeSetId": "<CHANGE_SET_ID>",
    "ChangeSetArn": "arn:aws:aws-marketplace:us-east-1:<AWS_ACCOUNT_ID>:AWSMarketplace/ChangeSet/<CHANGE_SET_ID>",
    "ChangeSetName": "Submitted by <AWS_ACCOUNT_ID>",
    "StartTime": "...",
    "EndTime": "...",
    "Status": "SUCCEEDED",
    "ChangeSet": [
        {
            "ChangeType": "<CHANGE_TYPE_NAME>",
            "Entity": {
                "Type": "AmiProduct@1.0",
                "Identifier": "<ENTITY_ID>"
            },
            "Details": "...",
            "ErrorDetailList": []
        }
    ]
}
```

**ChangeSet with user errors**
```json
{
    "ChangeSetId": "<CHANGE_SET_ID>",
    "ChangeSetArn": "arn:aws:aws-marketplace:us-east-1:<AWS_ACCOUNT_ID>:AWSMarketplace/ChangeSet/<CHANGE_SET_ID>",
    "ChangeSetName": "Submitted by <AWS_ACCOUNT_ID>",
    "StartTime": "...",
    "EndTime": "...",
    "Status": "FAILED",
    "FailureCode": "CLIENT_ERROR",
    "FailureDescription": "Change set preparation has failed. For details see 'ErrorDetailList'.",
    "ChangeSet": [
        {
            "ChangeType": "<CHANGE_TYPE_NAME>",
            "Entity": {
                "Type": "AmiProduct@1.0",
                "Identifier": "<ENTITY_ID>"
            },
            "Details": "...",
            "ErrorDetailList": [
                {
                    "ErrorCode": "SAMPLE_ERROR_CODE",
                    "ErrorMessage": "Sample description of error"
                }
            ]
        }
    ]
}
```