# Logging Elastic Transcoder API Calls Using CloudTrail<a name="logging_using_cloudtrail"></a>

Elastic Transcoder is integrated with CloudTrail, an AWS service that captures information about every request that is sent to the Elastic Transcoder API by your AWS account, including your IAM users\. CloudTrail periodically saves log files of these requests to an Amazon S3 bucket that you specify\. CloudTrail captures information about all requests, whether they were made using the Elastic Transcoder console, the Elastic Transcoder API, the AWS SDKs, the Elastic Transcoder CLI, or another service, for example, CloudFront\.

You can use information in the CloudTrail log files to determine which requests were made to Elastic Transcoder, the source IP address from which each request was made, who made the request, when it was made, and so on\. To learn more about CloudTrail, including how to configure and enable it, see the *[AWS CloudTrail User Guide](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/)*\.


+ [Elastic Transcoder Information in CloudTrail Log Files](#cloudfront_info_in_cloudtrail)
+ [Understanding Elastic Transcoder Log File Entries](#understanding_cloudfront_entries)

## Elastic Transcoder Information in CloudTrail Log Files<a name="cloudfront_info_in_cloudtrail"></a>

When you enable CloudTrail, CloudTrail captures every request that you make to every AWS service that CloudTrail supports\. \(For a list of supported services, see [ Supported Services](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/what_is_cloud_trail_supported_services.html) in the *AWS CloudTrail User Guide*\.\) CloudTrail saves the captured requests in log files in each region separately, and stores them in an Amazon S3 bucket\. The log files aren't organized or sorted by service; each log file might contain records from more than one service\. CloudTrail determines when to create a new log file\.

**Note**  
CloudTrail supports all Elastic Transcoder API actions\.

Every log file entry contains information about who made the request\. The user identity information in the log file helps you determine whether the request was made using root or IAM user credentials, using temporary security credentials for a role or federated user, or by another AWS service\. For more information, see [userIdentity Element](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/event_reference_user_identity.html) in the *AWS CloudTrail User Guide*\.

You can store log files for as long as you want\. You can also define Amazon S3 life cycle rules to archive or delete log files automatically\.

By default, your log files are encrypted by using Amazon S3 server\-side encryption \(SSE\)\.

You can choose to have CloudTrail publish Amazon SNS notifications when new log files are delivered if you want to take quick action upon log file delivery\. For more information, see [Configuring Amazon SNS Notifications](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html) in the *AWS CloudTrail User Guide*\.

You can also aggregate log files from multiple AWS regions and multiple AWS accounts into a single Amazon S3 bucket\. For more information, see [Aggregating CloudTrail Log Files to a Single Amazon S3 Bucket](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/aggregating_logs_top_level.html) in the *AWS CloudTrail User Guide*\. 

There is no cost to use the CloudTrail service\. However, standard rates for Amazon S3 usage apply as well as rates for Amazon SNS usage should you include that option\. For pricing details, see the [Amazon S3](http://aws.amazon.com/s3/pricing/) and [Amazon SNS](http://aws.amazon.com/sns/pricing/) pricing pages\.

## Understanding Elastic Transcoder Log File Entries<a name="understanding_cloudfront_entries"></a>

Each JSON\-formatted CloudTrail log file can contain one or more log entries\. A log entry represents a single request from any source and includes information about the requested action, including any parameters, the date and time of the action, and so on\. The log entries are not guaranteed to be in any particular order; they are not an ordered stack trace of API calls\.

The `eventSource` element identifies the source of the action that occurred\. For example, the following `eventSource` value indicates that Elastic Transcoder was called:

`elastictranscoder.amazonaws.com`

The `eventName` element identifies the action that occurred\. For example, the following `eventName` value indicates that a job was created:

`CreateJob`

The following example shows a CloudTrail log entry that demonstrates five actions:

+ Creating a job\. The value of `eventName` is `CreateJob`\.

+ Listing jobs by status\. The value of `eventName` is `ListJobsByStatus`\.

+ Getting a job\. The value of `eventName` is `ReadJob`\.

+ Deleting a Preset\. The value of `eventName` is `DeletePreset`\.

+ Deleting a pipeline\. The value of `eventName` is `DeletePipeline`\.

```
{
    "Records": [
        {
            "eventVersion": "1.02",
            "userIdentity": {
                "type": "IAMUser",
                "principalId": "A1B2C3D4E5F6G7EXAMPLE",
                "arn": "arn:aws:iam::111122223333:user/smithj",
                "accountId": "111122223333",
                "accessKeyId": "AKIAIOSFODNN7EXAMPLE"
            },
            "eventTime": "2014-09-29T19:29:02Z",
            "eventSource": "elastictranscoder.amazonaws.com",
            "eventName": "CreateJob",
            "awsRegion": "us-east-2",
            "sourceIPAddress": "192.0.2.17",
            "userAgent": "aws-sdk-ruby/1.39.0 ruby/1.9.3 x86_64-linux",
            "requestParameters": {
                "input": {
                    "interlaced": "auto",
                    "resolution": "auto",
                    "frameRate": "auto",
                    "aspectRatio": "auto",
                    "container": "auto",
                    "key": "source/audio/cheesytoast.wav"
                },
                "output": {
                    "presetId": "1234-preset-example",
                    "key": "output/testing-toast.mp4",
                    "thumbnailPattern": "",
                    "rotate": "auto"
                },
                "pipelineId": "1234-pipeline-example"
            },
            "responseElements": {
                "job": {
                    "output": {
                        "rotate": "auto",
                        "presetId": "1234-preset-example",
                        "thumbnailPattern": "",
                        "watermarks": [],
                        "id": "1",
                        "key": "output/testing-toast.mp4",
                        "status": "Submitted"
                    },
                    "status": "Submitted",
                    "playlists": [],
                    "arn": "arn:aws:elastictranscoder:us-east-2:111122223333:job/1234-job-example",
                    "id": "1234-job-example",
                    "outputs": [
                        {
                            "rotate": "auto",
                            "presetId": "1234-preset-example",
                            "thumbnailPattern": "",
                            "watermarks": [],
                            "id": "1",
                            "key": "output/testing-toast.mp4",
                            "status": "Submitted"
                        }
                    ],
                    "pipelineId": "1234-pipeline-example",
                    "input": {
                        "interlaced": "auto",
                        "resolution": "auto",
                        "frameRate": "auto",
                        "aspectRatio": "auto",
                        "container": "auto",
                        "key": "source/audio/cheesytoast.wav"
                    }
                }
            },
            "requestID": "4e6b66f9-d548-11e3-a8a9-73e33example",
            "eventID": "5ab02562-0fc5-43d0-b7b6-90293example",
            "eventType": "AwsApiCall",
            "recipientAccountId": "111122223333"
        },
        {
            "eventVersion": "1.02",
            "userIdentity": {
                "type": "IAMUser",
                "principalId": "A1B2C3D4E5F6G7EXAMPLE",
                "arn": "arn:aws:iam::111122223333:user/smithj",
                "accountId": "111122223333",
                "accessKeyId": "AKIAIOSFODNN7EXAMPLE"
            },
            "eventTime": "2014-09-29T19:29:18Z",
            "eventSource": "elastictranscoder.amazonaws.com",
            "eventName": "ListJobsByStatus",
            "awsRegion": "us-east-2",
            "sourceIPAddress": "192.0.2.17",
            "userAgent": "aws-sdk-ruby/1.39.0 ruby/1.9.3 x86_64-linux",
            "requestParameters": {
                "status": "Submitted",
                "ascending": "false"
            },
            "responseElements": null,
            "requestID": "52de9f97-d548-11e3-8fb9-4dad0example",
            "eventID": "eb91f423-6dd3-4bb0-a148-3cdfbexample",
            "eventType": "AwsApiCall",
            "recipientAccountId": "111122223333"
        },
        {
            "eventVersion": "1.02",
            "userIdentity": {
                "type": "IAMUser",
                "principalId": "A1B2C3D4E5F6G7EXAMPLE",
                "arn": "arn:aws:iam::111122223333:user/smithj",
                "accountId": "111122223333",
                "accessKeyId": "AKIAIOSFODNN7EXAMPLE"
            },
            "eventTime": "2014-09-29T19:28:50Z",
            "eventSource": "elastictranscoder.amazonaws.com",
            "eventName": "ReadJob",
            "awsRegion": "us-east-2",
            "sourceIPAddress": "192.0.2.17",
            "userAgent": "aws-sdk-ruby/1.39.0 ruby/1.9.3 x86_64-linux",
            "requestParameters": {
                "id": "1412018849233-f2czlr"
            },
            "responseElements": null,
            "requestID": "497b3622-d548-11e3-8fb9-4dad0example",
            "eventID": "c32289c7-005a-46f7-9801-cba41example",
            "eventType": "AwsApiCall",
            "recipientAccountId": "111122223333"
        },
        {
            "eventVersion": "1.02",
            "userIdentity": {
                "type": "IAMUser",
                "principalId": "A1B2C3D4E5F6G7EXAMPLE",
                "arn": "arn:aws:iam::111122223333:user/smithj",
                "accountId": "111122223333",
                "accessKeyId": "AKIAIOSFODNN7EXAMPLE"
            },
            "eventTime": "2014-09-29T19:29:18Z",
            "eventSource": "elastictranscoder.amazonaws.com",
            "eventName": "DeletePreset",
            "awsRegion": "us-east-2",
            "sourceIPAddress": "192.0.2.17",
            "userAgent": "aws-sdk-ruby/1.39.0 ruby/1.9.3 x86_64-linux",
            "requestParameters": {
                "id": "1234-preset-example"
            },
            "responseElements": null,
            "requestID": "4e200613-d548-11e3-a8a9-73e33example",
            "eventID": "191ebb93-66b7-4517-a741-92b0eexample",
            "eventType": "AwsApiCall",
            "recipientAccountId": "111122223333"
        },
        {
            "eventVersion": "1.02",
            "userIdentity": {
                "type": "IAMUser",
                "principalId": "A1B2C3D4E5F6G7EXAMPLE",
                "arn": "arn:aws:iam::111122223333:user/smithj",
                "accountId": "111122223333",
                "accessKeyId": "AKIAIOSFODNN7EXAMPLE"
            },
            "eventTime": "2014-09-29T19:29:01Z",
            "eventSource": "elastictranscoder.amazonaws.com",
            "eventName": "DeletePipeline",
            "awsRegion": "us-east-2",
            "sourceIPAddress": "192.0.2.17",
            "userAgent": "aws-sdk-ruby/1.39.0 ruby/1.9.3 x86_64-linux",
            "requestParameters": {
                "id": "1412018848038-nkomx0"
            },
            "responseElements": null,
            "requestID": "42ca4299-d548-11e3-8fb9-4dad0example",
            "eventID": "7aeb434f-eb55-4e2a-82d8-417d5example",
            "eventType": "AwsApiCall",
            "recipientAccountId": "111122223333"
        },
    ]
}
```