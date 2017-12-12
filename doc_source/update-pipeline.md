# Update Pipeline<a name="update-pipeline"></a>


+ [Description](#update-pipeline-description)
+ [How to Update and Delete Values](#update-pipeline-how-to)
+ [Requests](#update-pipeline-requests)
+ [Responses](#update-pipeline-responses)
+ [Errors](#update-pipeline-response-errors)
+ [Examples](#update-pipeline-examples)

## Description<a name="update-pipeline-description"></a>

To update settings for a pipeline, send a PUT request to the `/2012-09-25/pipelines/`*pipelineId* resource\.

**Important**  
When you change pipeline settings, your changes take effect immediately\. Jobs that you have already submitted and that Elastic Transcoder has not started to process are affected in addition to jobs that you submit after you change settings\.

## How to Update and Delete Values<a name="update-pipeline-how-to"></a>

To update a value, specify the new value, for example:

`"GranteeType":"Canonical"`

To leave a value unchanged, do one of the following:

+ Specify the current value\.

+ Specify a null value\. This applies both to individual objects \(for example, `"Role":null`\) and to arrays \(for example, `"ContentConfig":null`\)\.

+ Omit the JSON object from the request\. This applies both to individual objects, for example, `Role`, and to arrays, for example, `ContentConfig`\.

To delete the current value, specify an empty value\. For example, to delete a notification, specify an empty string: `"Progressing":""`\. To delete all of the values in an array, specify an empty array: `"Permissions":[]`\.

For example, if you no longer want to be notified when Elastic Transcoder encounters a warning while processing a job, and you don't want to change any of the other notification settings, you would specify the following for `Notifications` in the request:

```
...
"Notifications":{
   "Warning":""
},
...
```

## Requests<a name="update-pipeline-requests"></a>

### Syntax<a name="update-pipeline-request-syntax"></a>

```
PUT /2012-09-25/pipelines/pipelineId HTTP/1.1
Content-Type: application/json; charset=UTF-8
Accept: */*
Host: elastictranscoder.Elastic Transcoder endpoint.amazonaws.com:443
x-amz-date: 20130114T174952Z
Authorization: AWS4-HMAC-SHA256 
               Credential=AccessKeyID/request-date/Elastic Transcoder endpoint/elastictranscoder/aws4_request,
               SignedHeaders=host;x-amz-date;x-amz-target,
               Signature=calculated-signature
Content-Length: number of characters in the JSON string
{
   "[Id](#update-pipeline-request-id)":"pipelineId",
   "[Name](#update-pipeline-request-name)":"pipeline name",
   "[InputBucket](#update-pipeline-request-inputbucket)":"Amazon S3 bucket that contains files to transcode
      and graphics to use as watermarks",
   "[OutputBucket](#update-pipeline-request-outputbucket)":"Use this, or use ContentConfig:Bucket plus 
      ThumbnailConfig:Bucket",
   "[Role](#update-pipeline-request-role)":"IAM role ARN",
   "[AwsKmsKeyArn](#update-pipeline-request-kms-key-arn)":"AWS-KMS key ARN of the AWS-KMS key you want to 
      use with this pipeline",
   "Notifications":{
      "[Progressing](#update-pipeline-request-notifications-progressing)":"SNS topic to notify when
         Elastic Transcoder has started to process the job",
      "[Completed](#update-pipeline-request-notifications-completed)":"SNS topic to notify when
         Elastic Transcoder has finished processing the job",
      "[Warning](#update-pipeline-request-notifications-warning)":"SNS topic to notify when
         Elastic Transcoder encounters a warning condition"
      "[Error](#update-pipeline-request-notifications-error)":"SNS topic to notify when
         Elastic Transcoder encounters an error condition"
   },
   "[ContentConfig](#update-pipeline-request-contentconfig)":{
      "[Bucket](#update-pipeline-request-contentconfig-bucket)":"Use this plus ThumbnailConfig:Bucket,
         or use OutputBucket",
      "[Permissions](#update-pipeline-request-contentconfig-permissions)":[
         {
            "[GranteeType](#update-pipeline-request-contentconfig-granteetype)":"Canonical|Email|Group",
            "[Grantee](#update-pipeline-request-contentconfig-grantee)":"AWS user ID or CloudFront origin access identity"|
                      "registered email address for AWS account|
                      AllUsers|AuthenticatedUsers|LogDelivery",
            "[Access](#update-pipeline-request-contentconfig-access)":[
               "Read|ReadAcp|WriteAcp|FullControl",
               ...
            ]
         },
         {...}
      ],
      "[StorageClass](#update-pipeline-request-contentconfig-storageclass)":"Standard|ReducedRedundancy"
   },
   "[ThumbnailConfig](#update-pipeline-request-thumbnailconfig)":{
      "[Bucket](#update-pipeline-request-thumbnailconfig-bucket)":"Use this plus ContentConfig:Bucket,
         or use OutputBucket",
      "[Permissions](#update-pipeline-request-thumbnailconfig-permissions)":[
         {
            "[GranteeType](#update-pipeline-request-thumbnailconfig-granteetype)":"Canonical|Email|Group",
            "[Grantee](#update-pipeline-request-thumbnailconfig-grantee)":"AWS user ID or CloudFront origin access identity"|
                      "registered email address for AWS account|
                      AllUsers|AuthenticatedUsers|LogDelivery",
            "[Access](#update-pipeline-request-thumbnailconfig-access)":[
               "Read|ReadAcp|WriteAcp|FullControl",
               ...
            ]
         },
         {...}
      ],
      "[StorageClass](#update-pipeline-request-thumbnailconfig-storageclass)":"Standard|ReducedRedundancy"
   },
   "[Status](#update-pipeline-request-status)":"Active|Paused"
}
```

### Request Parameters<a name="update-pipeline-request-parameters"></a>

This operation does not use request parameters\.

### Request Headers<a name="update-pipeline-request-headers"></a>

This operation uses only request headers that are common to all operations\. For information about common request headers, see [HTTP Header Contents](making-http-requests.md#http-request-header)\.

### Request Body<a name="update-pipeline-request-body"></a>

The JSON string in the request body contains the following objects\. 

**Id**  
Identifier for the pipeline\. You use this value to identify the pipeline in which you want to perform a variety of operations, for example, creating a job or a preset\. 

**Name**  
The name of the pipeline\. We recommend that the name be unique within the AWS account, but uniqueness is not enforced\.  
Constraints: Maximum 40 characters

**InputBucket**  
The Amazon S3 bucket in which you saved the media files that you want to transcode and the graphics that you want to use as watermarks\.

**OutputBucket \(Use this, or use ContentConfig:Bucket plus ThumbnailConfig:Bucket\)**  
The Amazon S3 bucket in which you want Elastic Transcoder to save the transcoded files\. Specify this value when all of the following are true:  

+ You want to save transcoded files, thumbnails \(if any\), and playlists \(if any\) together in one bucket\.

+ You do not want to specify the users or groups who have access to the transcoded files, thumbnails, and playlists\.

+ You do not want to specify the permissions that Elastic Transcoder grants to the files\.
**Note**  
When Elastic Transcoder saves files in `OutputBucket`, it grants full control over the files only to the AWS account that owns the role that is specified by `Role`\.

+ You want to associate the transcoded files and thumbnails with the Amazon S3 `Standard` storage class\.
If you want to save transcoded files and playlists in one bucket and thumbnails in another bucket, specify which users can access the transcoded files or the permissions the users have, or change the Amazon S3 storage class, omit `OutputBucket` and specify values for `ContentConfig` and `ThumbnailConfig` instead\. 

**Role**  
The IAM Amazon Resource Name \(ARN\) for the role that you want Elastic Transcoder to use to transcode jobs for this pipeline\.

**\(Optional\) AwsKmsKeyArn**  
The AWS Key Management Service \(AWS KMS\) key that you want to use with this pipeline\.  
If you use either **s3** or **s3\-aws\-kms** as your **Encryption:Mode**, you don't need to provide a key with your job because a default key, known as an AWS\-KMS key, is created for you automatically\. You need to provide an AWS\-KMS key only if you want to use a non\-default AWS\-KMS key, or if you are using an **Encryption:Mode** of **aes\-pkcs7**, **aes\-ctr**, or **aes\-gcm**\.

**Notifications:Progressing**  
The topic ARN for the Amazon Simple Notification Service \(Amazon SNS\) topic that you want to notify when Elastic Transcoder has started to process a job in this pipeline\. This is the ARN that Amazon SNS returned when you created the topic\. For more information, see [Create a Topic](http://docs.aws.amazon.com/sns/latest/dg/CreateTopic.html) in the *Amazon Simple Notification Service Developer Guide*\.  
To receive notifications, you must also subscribe to the new topic in the Amazon SNS console\.
Amazon SNS offers a variety of notification options, including the ability to send Amazon SNS messages to Amazon Simple Queue Service queues\. For more information, see the [Amazon Simple Notification Service Developer Guide](http://docs.aws.amazon.com/sns/latest/dg/)\.

**Notifications:Completed**  
The topic ARN for the Amazon SNS topic that you want to notify when Elastic Transcoder has finished processing a job in this pipeline\. This is the ARN that Amazon SNS returned when you created the topic\. 

**Notifications:Warning**  
The topic ARN for the Amazon SNS topic that you want to notify when Elastic Transcoder encounters a warning condition while processing a job in this pipeline\. This is the ARN that Amazon SNS returned when you created the topic\. 

**Notifications:Error**  
The topic ARN for the Amazon SNS topic that you want to notify when Elastic Transcoder encounters an error condition while processing a job in this pipeline\. This is the ARN that Amazon SNS returned when you created the topic\. 

**ContentConfig \(Use this plus ThumbnailConfig, or use OutputBucket\)**  
The `ContentConfig` object specifies information about the Amazon S3 bucket in which you want Elastic Transcoder to save transcoded files and playlists: which bucket to use, which users you want to have access to the files, the type of access you want users to have, and the storage class that you want to assign to the files\.   
If you specify values for `ContentConfig`, you must also specify values for `ThumbnailConfig>`\.  
If you specify values for `ContentConfig` and `ThumbnailConfig`, omit the `OutputBucket` object\.

**ContentConfig:Bucket**  
The Amazon S3 bucket in which you want Elastic Transcoder to save transcoded files and playlists\.

**\(Optional\) ContentConfig:Permissions**  
The `Permissions` object specifies which users and/or predefined Amazon S3 groups you want to have access to transcoded files and playlists, and the type of access you want them to have\. You can grant permissions to a maximum of 30 users and/or predefined Amazon S3 groups\.   
If you include `Permissions`, Elastic Transcoder grants only the permissions that you specify\. It does not grant full permissions to the owner of the role specified by `Role`\. If you want that user to have full control, you must explicitly grant full control to the user\.  
If you omit `Permissions`, Elastic Transcoder grants full control over the transcoded files and playlists to the owner of the role specified by `Role`, and grants no other permissions to any other user or group\.

**ContentConfig:Permissions:GranteeType**  
Specify the type of value that appears in the `ContentConfig:Permissions:Grantee` object:  

+ **Canonical:** The value in the `Grantee` object is either the canonical user ID for an AWS account or an origin access identity for an Amazon CloudFront distribution\. For more information about canonical user IDs, see [Access Control List \(ACL\) Overview](http://docs.aws.amazon.com/AmazonS3/latest/dev/ACLOverview.html) in the *Amazon Simple Storage Service Developer Guide*\. For more information about using CloudFront origin access identities to require that users use CloudFront URLs instead of Amazon S3 URLs, see [Using an Origin Access Identity to Restrict Access to Your Amazon S3 Content](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html)\.
**Important**  
A canonical user ID is not the same as an AWS account number\.

+ **Email:** The value in the `Grantee` object is the registered email address of an AWS account\.

+ **Group:** The value in the `Grantee` object is one of the following predefined Amazon S3 groups: `AllUsers`, `AuthenticatedUsers`, or `LogDelivery`\.

**ContentConfig:Permissions:Grantee**  
The AWS user or group that you want to have access to transcoded files and playlists\. To identify the user or group, you can specify the canonical user ID for an AWS account, an origin access identity for a CloudFront distribution, the registered email address of an AWS account, or a predefined Amazon S3 group\. For more information, see `ContentConfig:Permissions:GranteeType`\.

**ContentConfig:Permissions:Access**  
The permission that you want to give to the AWS user that you specified in `ContentConfig:Permissions:Grantee`\. Permissions are granted on the files that Elastic Transcoder adds to the bucket, including playlists, video files, and audio files\. The following values are valid:  

+ **`Read`:** The grantee can read the objects and metadata for objects that Elastic Transcoder adds to the Amazon S3 bucket\.

+ **`ReadAcp`:** The grantee can read the object ACL for objects that Elastic Transcoder adds to the Amazon S3 bucket\.

+ **`WriteAcp`:** The grantee can write the ACL for the objects that Elastic Transcoder adds to the Amazon S3 bucket\.

+ **`FullControl`:** The grantee has `Read`, `ReadAcp`, and `WriteAcp` permissions for the objects that Elastic Transcoder adds to the Amazon S3 bucket\.

**ContentConfig:StorageClass**  
The Amazon S3 storage class, `Standard` or `ReducedRedundancy`, that you want Elastic Transcoder to assign to the files and playlists that it stores in your Amazon S3 bucket\. For more information, see [Reduced Redundancy Storage](http://docs.aws.amazon.com/AmazonS3/latest/dev/Introduction.html#RRS) in the *Amazon Simple Storage Service Developer Guide*\. 

**ThumbnailConfig \(Use this plus ContentConfig, or use OutputBucket\)**  
The `ThumbnailConfig` object specifies information about the Amazon S3 bucket in which you want Elastic Transcoder to save thumbnail files: which bucket to use, which users you want to have access to the files, the type of access you want users to have, and the storage class that you want to assign to the files\.   
If you specify values for `ContentConfig`, you must also specify values for `ThumbnailConfig` even if you don't want to create thumbnails\. \(You control whether to create thumbnails when you create a job\. For more information, see [ThumbnailPattern](create-job.md#create-job-request-output-thumbnail-pattern) in the topic [Create Job](create-job.md)\.\)  
If you specify values for `ContentConfig` and `ThumbnailConfig`, omit the `OutputBucket` object\.

**ThumbnailConfig:Bucket**  
The Amazon S3 bucket in which you want Elastic Transcoder to save thumbnail files\. 

**\(Optional\) ThumbnailConfig:Permissions**  
The `Permissions` object specifies which users and/or predefined Amazon S3 groups you want to have access to thumbnail files, and the type of access you want them to have\. You can grant permissions to a maximum of 30 users and/or predefined Amazon S3 groups\.   
If you include `Permissions`, Elastic Transcoder grants only the permissions that you specify\. It does not grant full permissions to the owner of the role specified by `Role`\. If you want that user to have full control, you must explicitly grant full control to the user\.  
If you omit `Permissions`, Elastic Transcoder grants full control over the thumbnails to the owner of the role specified by `Role`, and grants no other permissions to any other user or group\.

**ThumbnailConfig:Permissions:GranteeType**  
Specify the type of value that appears in the `ThumbnailConfig:Permissions:Grantee` object:  

+ **Canonical:** The value in the `Grantee` object is either the canonical user ID for an AWS account or an origin access identity for an Amazon CloudFront distribution\. For more information about canonical user IDs, see [Access Control List \(ACL\) Overview](http://docs.aws.amazon.com/AmazonS3/latest/dev/ACLOverview.html) in the *Amazon Simple Storage Service Developer Guide*\. For more information about using CloudFront origin access identities to require that users use CloudFront URLs instead of Amazon S3 URLs, see [Using an Origin Access Identity to Restrict Access to Your Amazon S3 Content](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html)\.
**Important**  
A canonical user ID is not the same as an AWS account number\.

+ **Email:** The value in the `Grantee` object is the registered email address of an AWS account\.

+ **Group:** The value in the `Grantee` object is one of the following predefined Amazon S3 groups: `AllUsers`, `AuthenticatedUsers`, or `LogDelivery`\.

**ThumbnailConfig:Permissions:Grantee**  
The AWS user or group that you want to have access to thumbnail files\. To identify the user or group, you can specify the canonical user ID for an AWS account, an origin access identity for a CloudFront distribution, the registered email address of an AWS account, or a predefined Amazon S3 group\. For more information, see `ThumbnailConfig:Permissions:GranteeType`\.

**ThumbnailConfig:Permissions:Access**  
The permission that you want to give to the AWS user that you specified in `ThumbnailConfig:Permissions:Grantee`\. Permissions are granted on the thumbnail files that Elastic Transcoder adds to the bucket\. The following values are valid:  

+ **`Read`:** The grantee can read the thumbnails and metadata for thumbnails that Elastic Transcoder adds to the Amazon S3 bucket\.

+ **`ReadAcp`:** The grantee can read the object ACL for thumbnails that Elastic Transcoder adds to the Amazon S3 bucket\.

+ **`WriteAcp`:** The grantee can write the ACL for the thumbnails that Elastic Transcoder adds to the Amazon S3 bucket\.

+ **`FullControl`:** The grantee has `Read`, `ReadAcp`, and `WriteAcp` permissions for the thumbnails that Elastic Transcoder adds to the Amazon S3 bucket\.

**ThumbnailConfig:StorageClass**  
The Amazon S3 storage class, `Standard` or `ReducedRedundancy`, that you want Elastic Transcoder to assign to the thumbnails that it stores in your Amazon S3 bucket\. For more information, see [Reduced Redundancy Storage](http://docs.aws.amazon.com/AmazonS3/latest/dev/Introduction.html#RRS) in the *Amazon Simple Storage Service Developer Guide*\.

**Status**  
The current status of the pipeline:  

+ `Active`: The pipeline is processing jobs\.

+ `Paused`: The pipeline is not currently processing jobs\.

## Responses<a name="update-pipeline-responses"></a>

### Syntax<a name="update-pipeline-response-syntax"></a>

```
Status: 202 Accepted
x-amzn-RequestId: c321ec43-378e-11e2-8e4c-4d5b971203e9
Content-Type: application/json
Content-Length: number of characters in the response
Date: Mon, 14 Jan 2013 06:01:47 GMT

{
   "Id":"Id for the new pipeline",
   "Name":"pipeline name",
   "InputBucket":"Amazon S3 bucket that contains files to transcode
      and graphics to use as watermarks",
   "OutputBucket":"Use this, or use ContentConfig:Bucket plus 
      ThumbnailConfig:Bucket",
   "Role":"IAM role ARN",
   "AwsKmsKeyArn":"AWS-KMS key id",
   "Notifications":{
      "Progressing":"SNS topic to notify when
         when Elastic Transcoder has started to process the job",
      "Completed":"SNS topic to notify when
         Elastic Transcoder has finished processing the job",
      "Warning":"SNS topic to notify when
         when Elastic Transcoder encounters a warning condition",
      "Error":"SNS topic to notify when
         Elastic Transcoder encounters an error condition"
   },
   "ContentConfig":{
      "Bucket":"Use this plus ThumbnailConfig:Bucket,
         or use OutputBucket",
      "Permissions":[
         {
            "GranteeType":"Canonical|Email|Group",
            "Grantee":"AWS user ID or CloudFront origin access identity"|
                      "registered email address for AWS account|
                      AllUsers|AuthenticatedUsers|LogDelivery",
            "Access":[
               "Read|ReadAcp|WriteAcp|FullControl",
               ...
            ]
         },
         {...}
      ],
      "StorageClass":"Standard|ReducedRedundancy"
   },
   "ThumbnailConfig":{
      "Bucket":"Use this plus ContentConfig:Bucket,
         or use OutputBucket",
      "Permissions":[
         {
            "Access":[
               "Read|ReadAcp|WriteAcp|FullControl",
               ...
            ],
            "Grantee":"AWS user ID or CloudFront origin access identity"|
                      "registered email address for AWS account|
                      AllUsers|AuthenticatedUsers|LogDelivery",
            "GranteeType":"Canonical|Email|Group"
         },
         {...}
      ],
      "StorageClass":"Standard|ReducedRedundancy"
   },
   "Status":"Active|Paused",
   "[Warnings](#update-pipeline-response-warnings)": [
      {
         "[Code](#update-pipeline-response-warning-code)": "6000|6001|6002|6003|6004|6005|6006|6007|6008",
         "[Message](#update-pipeline-response-warning-message)": "The code message"
      },
      {...}
   ]
}
```

### Response Headers<a name="update-pipeline-response-headers"></a>

This operation uses only response headers that are common to most responses\. For information about common response headers, see [HTTP Responses](making-http-requests.md#http-response-header)\.

### Response Body<a name="update-pipeline-response-body"></a>

When you create a pipeline, Elastic Transcoder returns the values that you specified in the request\. For more information, see [Request Body](#update-pipeline-request-body)\.

Elastic Transcoder will also include the following warnings, if applicable:

#### Warnings<a name="update-pipeline-response-warnings"></a>

When you create a pipeline that uses resources in other regions, Elastic Transcoder returns one or more warnings\. Your pipeline is still created, but might have increased processing times and incur cross\-regional charges\. The warnings are in the following format:

**Code**  
**Message** — the message associated with the warning code\.

The following is a list of valid warning codes and their messages:

**6000**  
The input bucket and the pipeline are in different regions, which increases processing time for jobs in the pipeline and can incur additional charges\. To decrease processing time and prevent cross\-regional charges, use the same region for the input bucket and the pipeline\. 

**6001**  
The ContentConfig bucket and the pipeline are in different regions, which increases processing time for jobs in the pipeline and can incur additional charges\. To decrease processing time and prevent cross\-regional charges, use the same region for the ContentConfig bucket and the pipeline\. 

**6002**  
The ThumbnailConfig bucket and the pipeline are in different regions, which increases processing time for jobs in the pipeline and can incur additional charges\. To decrease processing time and prevent cross\-regional charges, use the same region for the ThumbnailConfig bucket and the pipeline\. 

**6003**  
The SNS notification topic for progressing events and the pipeline are in different regions, which increases processing time for jobs in the pipeline and can incur additional charges\. To decrease processing time and prevent cross\-regional charges, use the same region for the SNS notification topic and the pipeline\.

**6004**  
The SNS notification topic for warning events and the pipeline are in different regions, which increases processing time for jobs in the pipeline and can incur additional charges\. To decrease processing time and prevent cross\-regional charges, use the same region for the SNS notification topic and the pipeline\.

**6005**  
The SNS notification topic for completion events and the pipeline are in different regions, which increases processing time for jobs in the pipeline and can incur additional charges\. To decrease processing time and prevent cross\-regional charges, use the same region for the SNS notification topic and the pipeline\.

**6006**  
The SNS notification topic for error events and the pipeline are in different regions, which increases processing time for jobs in the pipeline and can incur additional charges\. To decrease processing time and prevent cross\-regional charges, use the same region for the SNS notification topic and the pipeline\. 

**6007**  
The AWS KMS key and ContentConfig bucket specified for this pipeline are in different regions, which causes outputs using s3\-aws\-kms encryption mode to fail\. To use s3\-aws\-kms encryption mode, use the same region for the KMS key and the ContentConfig bucket\. 

**6008**  
The AWS KMS key and ThumbnailConfig bucket specified for this pipeline are in different regions, which causes outputs using s3\-aws\-kms encryption mode to fail\. To use s3\-aws\-kms encryption mode, use the same region for the KMS key and the ThumbnailConfig bucket\. 

## Errors<a name="update-pipeline-response-errors"></a>

For information about Elastic Transcoder exceptions and error messages, see [Handling Errors in Elastic Transcoder](error-handling.md)\.

## Examples<a name="update-pipeline-examples"></a>

The following example request updates the pipeline that has the Id `1111111111111-abcde1`\.

### Sample Request<a name="update-pipeline-examples-sample-request"></a>

```
PUT /2012-09-25/pipelines/1111111111111-abcde1 HTTP/1.1
Content-Type: application/json; charset=UTF-8
Accept: */*
Host: elastictranscoder.Elastic Transcoder endpoint.amazonaws.com:443
x-amz-date: 20130114T174952Z
Authorization: AWS4-HMAC-SHA256 
               Credential=AccessKeyID/request-date/Elastic Transcoder endpoint/elastictranscoder/aws4_request,
               SignedHeaders=host;x-amz-date;x-amz-target,
               Signature=calculated-signature
Content-Length: number of characters in the JSON string
{  
   "Id":"1111111111111-abcde1"
   "Name":"Default",
   "InputBucket":"salesoffice.example.com-source",
   "OutputBucket":"salesoffice.example.com-output",
   "Role":"arn:aws:iam::123456789012:role/Elastic_Transcoder_Default_Role",
   "AwsKmsKeyArn":"base64 encoded key from KMS",
   "Notifications":{
      "Progressing":"",
      "Completed":"",
      "Warning":"",
      "Error":"arn:aws:sns:us-east-1:111222333444:ET_Errors"
   },
   "ContentConfig":{
      "Bucket":"salesoffice.example.com-public-promos",
      "Permissions":[
         {
            "GranteeType":"Email",
            "Grantee":"marketing-promos@example.com",
            "Access":[
               "FullControl"
            ]
         }
      ],
      "StorageClass":"Standard"
   },
   "ThumbnailConfig":{
      "Bucket":"salesoffice.example.com-public-promos-thumbnails",
      "Permissions":[
         {
            "GranteeType":"Email",
            "Grantee":"marketing-promos@example.com",
            "Access":[
               "FullControl"
            ]
         }
      ],
      "StorageClass":"ReducedRedundancy"
   },
   "Status":"Active"
}
```

### Sample Response<a name="update-pipeline-examples-sample-response"></a>

```
Status: 202 Accepted
x-amzn-RequestId: c321ec43-378e-11e2-8e4c-4d5b971203e9
Content-Type: application/json
Content-Length: number of characters in the response
Date: Mon, 14 Jan 2013 06:01:47 GMT
{
   "Id":"1111111111111-abcde1",
   "Name":"Default",
   "InputBucket":"salesoffice.example.com-source",
   "OutputBucket":"salesoffice.example.com-output",
   "Role":"arn:aws:iam::123456789012:role/Elastic_Transcoder_Default_Role",
   "AwsKmsKeyArn":"base64 encoded key from KMS",
   "Notifications":{
      "Progressing":"",
      "Completed":"",
      "Warning":"",
      "Error":"arn:aws:sns:us-east-1:111222333444:ET_Errors"
   },
   "ContentConfig":{
      "Bucket":"salesoffice.example.com-public-promos",
      "Permissions":[
         {
            "GranteeType":"Email",
            "Grantee":"marketing-promos@example.com",
            "Access":[
               "FullControl"
            ]
         }
      ],
      "StorageClass":"Standard"
   },
   "ThumbnailConfig":{
      "Bucket":"salesoffice.example.com-public-promos-thumbnails",
      "Permissions":[
         {
            "GranteeType":"Email",
            "Grantee":"marketing-promos@example.com",
            "Access":[
               "FullControl"
            ]
         }
      ],
      "StorageClass":"ReducedRedundancy"
   },
   "Status":"Active",
   "Warnings": [
      {
         "Code": "6000",
         "Message": "The input bucket and the pipeline are in different 
            regions, which increases processing time for jobs in the 
            pipeline and can incur additional charges. To decrease 
            processing time and prevent cross-regional charges, use the 
            same region for the input bucket and the pipeline."
      },
      {...}
   ]
}
```