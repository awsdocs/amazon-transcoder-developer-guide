# List Jobs by Status<a name="list-jobs-by-status"></a>


+ [Description](#list-jobs-by-status-description)
+ [Requests](#list-jobs-by-status-requests)
+ [Responses](#list-jobs-by-status-responses)
+ [Errors](#list-jobs-by-status-response-errors)
+ [Examples](#list-jobs-by-status-examples)

## Description<a name="list-jobs-by-status-description"></a>

To get a list of the jobs that have a specified status, send a GET request to the `/2012-09-25/jobsByStatus/Submitted` resource\. Elastic Transcoder lists the jobs that you've created recently and that currently have the specified status\. 

## Requests<a name="list-jobs-by-status-requests"></a>

### Syntax<a name="list-jobs-by-status-request-syntax"></a>

To get information about all of the jobs associated with the current AWS account that have a specified status, send the following GET request\. 

```
GET /2012-09-25/jobsByStatus/[Status](#list-jobs-by-status-request-status)?
[Ascending](#list-jobs-by-status-request-ascending)=true|false&
[PageToken](#list-jobs-by-status-request-pageToken)=value for accessing the next page of results HTTP/1.1
Content-Type: charset=UTF-8
Accept: */*
Host: elastictranscoder.Elastic Transcoder endpoint.amazonaws.com:443
x-amz-date: 20130114T174952Z
Authorization: AWS4-HMAC-SHA256
               Credential=AccessKeyID/request-date/Elastic Transcoder endpoint/elastictranscoder/aws4_request,
               SignedHeaders=host;x-amz-date;x-amz-target,
               Signature=calculated-signature
```

### Request Parameters<a name="list-jobs-by-status-request-parameters"></a>

This operation takes the following request parameters\. Elastic Transcoder returns all of the jobs that have the specified status\.

**Status**  
To get information about all of the jobs associated with the current AWS account that have a given status, specify the status: `Submitted`, `Progressing`, `Complete`, `Canceled`, or `Error`\.

**Ascending**  
To list jobs in chronological order by the date and time that they were submitted, enter `true`\. To list jobs in reverse chronological order, enter `false`\.

**PageToken**  
When Elastic Transcoder returns more than one page of results, use `PageToken` in subsequent `GET` requests to get each successive page of results\.

### Request Headers<a name="list-jobs-by-status-request-headers"></a>

This operation uses only request headers that are common to all operations\. For information about common request headers, see [HTTP Header Contents](making-http-requests.md#http-request-header)\.

### Request Body<a name="list-jobs-by-status-request-body"></a>

This operation does not use a request body\. 

## Responses<a name="list-jobs-by-status-responses"></a>

### Syntax<a name="list-jobs-by-status-response-syntax"></a>

```
Status: 200 OK
x-amzn-RequestId: c321ec43-378e-11e2-8e4c-4d5b971203e9
Content-Type: application/json
Content-Length: number of characters in the response
Date: Mon, 14 Jan 2013 06:01:47 GMT

{
   "Jobs":[
      {
         "[Id](#list-jobs-by-status-response-job-id)":"Id that Elastic Transcoder assigned to the job",
         "[Inputs](#list-jobs-by-status-response-inputs)":[{
            "[Key](#list-jobs-by-status-response-inputs-key)":"name of the file to transcode",
            "[Encryption](#list-jobs-by-status-response-inputs-encryption)":{
               "[Mode](#list-jobs-by-status-response-inputs-encrypt-mode)":"aes-cbc-pkcs7|aes-ctr|aes-gcm",
               "[Key](#list-jobs-by-status-response-inputs-encrypt-key)":"encrypted and base64-encoded decryption key",
               "[KeyMd5](#list-jobs-by-status-response-inputs-encrypt-key-md5)":"base64-encoded key digest",
               "[InitializationVector](#list-jobs-by-status-response-inputs-encrypt-vector)":"base64-encoded initialization 
                  vector"
            },
            "[TimeSpan](#list-jobs-by-status-response-inputs-composition-clip-time-span)":{
               "[StartTime](#list-jobs-by-status-response-inputs-composition-clip-start-time)":"starting place of the clip, in
                  HH:mm:ss.SSS or sssss.SSS",
               "[Duration](#list-jobs-by-status-response-inputs-composition-clip-duration)":"duration of the clip, in HH:mm:ss.SSS
                  or sssss.SSS"
            },
            "[FrameRate](#list-jobs-by-status-response-inputs-frame-rate)":"auto|10|15|23.97|24|25|29.97|30|50|60",
            "[Resolution](#list-jobs-by-status-response-inputs-resolution)":"auto",
            "[AspectRatio](#list-jobs-by-status-response-inputs-aspect-ratio)":"auto|1:1|4:3|3:2|16:9",
            "[Interlaced](#list-jobs-by-status-response-inputs-interlaced)":"auto|true|false",
            "[Container](#list-jobs-by-status-response-inputs-container)":"auto|3gp|aac|asf|avi|divx|flv|m4a|mkv|mov|mp3|
               mp4|mpeg|mpeg-ps|mpeg-ts|mxf|ogg|vob|wav|webm",
            "[DetectedProperties](#list-jobs-by-status-response-inputs-detected-properties)":{
               "[Width](#list-jobs-by-status-response-inputs-detected-width)":"video width in pixels",
               "[Height](#list-jobs-by-status-response-inputs-detected-height)":"video height in pixels",          
               "[FrameRate](#list-jobs-by-status-response-inputs-detected-frame-rate)":"video frame rate in fps",
               "[FileSize](#list-jobs-by-status-response-inputs-detected-file-size)":"file size in bytes",
               "[DurationMillis](#list-jobs-by-status-response-inputs-detected-duration)":"file duration in milliseconds"
            },
            "[InputCaptions](#list-jobs-by-status-response-inputs-captions)":{
               "[MergePolicy](#list-jobs-by-status-response-inputs-captions-merge-policy)":"MergeOverride|MergeRetain|Override",
               "[CaptionSources](#list-jobs-by-status-response-inputs-captions-sources)":[
                  {
                     "[Key](#list-jobs-by-status-response-inputs-captions-key)":"name of the input caption file",
                     "[Encryption](#list-jobs-by-status-response-inputs-encryption)":{
                        "[Mode](#list-jobs-by-status-response-inputs-encrypt-mode)":"aes-cbc-pkcs7|aes-ctr|aes-gcm",
                        "[Key](#list-jobs-by-status-response-inputs-encrypt-key)":"encrypted and base64-encoded encryption key",
                        "[KeyMd5](#list-jobs-by-status-response-inputs-encrypt-key-md5)":"base64-encoded key digest",
                        "[InitializationVector](#list-jobs-by-status-response-inputs-encrypt-vector)":"base64-encoded 
                           initialization vector"
                     },
                     "[Language](#list-jobs-by-status-response-inputs-captions-language)":"language of the input caption file",
                     "[TimeOffset](#list-jobs-by-status-response-inputs-captions-time-offset)":"starting place of the captions, in
                        either [-+]SS.sss or [-+]HH:mm:SS.ss",
                     "[Label](#list-jobs-by-status-response-inputs-captions-label)":"label for the caption"
                  },
                  {...}
                  ]
               }
            },
            {...}
         ],
         "[OutputKeyPrefix](#list-jobs-by-status-response-output-key-prefix)":"prefix for file names in Amazon S3 bucket",
         "[Outputs](#list-jobs-by-status-response-outputs)":[
            {
               "[Id](#list-jobs-by-status-response-output-id)":"sequential counter",
               "[Key](#list-jobs-by-status-response-output-key)":"name of the transcoded file",
               "[Encryption](#list-jobs-by-status-response-output-encryption)":{
                  "[Mode](#list-jobs-by-status-response-output-encrypt-mode)":"s3|s3-aws-kms|aes-cbc-pkcs7|
                     aes-ctr|aes-gcm",
                  "[Key](#list-jobs-by-status-response-output-encrypt-key)":"encrypted and base64-encoded encryption key",
                  "[KeyMd5](#list-jobs-by-status-response-output-encrypt-key-md5)":"base64-encoded key digest",
                  "[InitializationVector](#list-jobs-by-status-response-output-encrypt-vector)":"base64-encoded initialization 
                     vector"
               },
               "[ThumbnailPattern](#list-jobs-by-status-response-output-thumbnail-pattern)":""|"pattern",
               "[Rotate](#list-jobs-by-status-response-output-rotate)":"auto|0|90|180|270",
               "[PresetId](#list-jobs-by-status-response-output-preset-id)":"PresetId for the job",
               "[SegmentDuration](#list-jobs-by-status-response-output-segment-duration)":"[1,60]",
               "[Watermarks](#list-jobs-by-status-response-output-watermarks)":[
                  {
                     "[InputKey](#list-jobs-by-status-response-output-watermarks-inputs-key)":"name of the .png or .jpg file",
                     "[PresetWatermarkId](#list-jobs-by-status-response-output-watermarks-preset-watermark-id)":"value of Video:Watermarks:Id in 
                        preset",
                     "[Encryption](#list-jobs-by-status-response-output-encryption)":{
                        "[Mode](#list-jobs-by-status-response-output-encrypt-mode)":"s3|s3-aws-kms|aes-cbc-pkcs7|
                           aes-ctr|aes-gcm",
                        "[Key](#list-jobs-by-status-response-output-encrypt-key)":"encrypted and base64-encoded encryption key",
                        "[KeyMd5](#list-jobs-by-status-response-output-encrypt-key-md5)":"base64-encoded key digest",
                        "[InitializationVector](#list-jobs-by-status-response-output-encrypt-vector)":"base64-encoded 
                           initialization vector"
                     }
                  },
                  {...}
               ],
               "[AlbumArt](#list-jobs-by-status-response-output-album-art)":[
                  {
                     "[AlbumArtMerge](#list-jobs-by-status-response-output-album-art-merge)":"Replace|Prepend|Append|Fallback",
                     "[AlbumArtArtwork](#list-jobs-by-status-response-output-album-art-artwork)":"can be empty, but not null":[
                        {
                           "[AlbumArtInputKey](#list-jobs-by-status-response-output-album-art-art-inputs-key)":"name of the file to use as
                              album art",
                           "[Encryption](#list-jobs-by-status-response-output-encryption)":{
                              "[Mode](#list-jobs-by-status-response-output-encrypt-mode)":"s3|s3-aws-kms|aes-cbc-pkcs7|
                                 aes-ctr|aes-gcm",
                              "[Key](#list-jobs-by-status-response-output-encrypt-key)":"encrypted and base64-encoded encryption 
                                 key",
                              "[KeyMd5](#list-jobs-by-status-response-output-encrypt-key-md5)":"base64-encoded key digest",
                              "[InitializationVector](#list-jobs-by-status-response-output-encrypt-vector)":"base64-encoded 
                                 initialization vector"
                           },
                           "[AlbumArtMaxWidth](#list-jobs-by-status-response-output-album-art-max-width)":"maximum width of output album
                              art in pixels",
                           "[AlbumArtMaxHeight](#list-jobs-by-status-response-output-album-art-max-height)":"maximum height of output
                              album art in pixels",
                           "[AlbumArtSizingPolicy](#list-jobs-by-status-response-output-album-art-sizing-policy)":"Fit|Fill|Stretch|Keep|
                              ShrinkToFit|ShrinkToFill",
                           "[AlbumArtPaddingPolicy](#list-jobs-by-status-response-output-album-art-padding-policy)":"Pad|NoPad",
                           "[AlbumArtFormat](#list-jobs-by-status-response-output-album-art-format)":"jpg|png"
                        },
                        {...}
                     ]
                   },
                  {...}
               ],
               "[Duration](#list-jobs-by-status-response-output-duration)":"duration in seconds",
               "[DurationMillis](#list-jobs-by-status-response-output-duration-millis)":"duration in milliseconds",
               "[Height](#list-jobs-by-status-response-output-height)":"height in pixels",
               "[Width](#list-jobs-by-status-response-output-width)":"width in pixels",
               "[FrameRate](#list-jobs-by-status-response-output-frame-rate)":"frame rate in fps",
               "[FileSize](#list-jobs-by-status-response-output-file-size)":"file size in bytes",
               "[Status](#list-jobs-by-status-response-output-status)":"Submitted|In Progress|Complete|Error",
               "[StatusDetail](#list-jobs-by-status-response-output-status-detail)":"detail associated with Status",
               "[Captions](#list-jobs-by-status-request-outputs-captions)":{
                  "[CaptionFormats](#list-jobs-by-status-request-outputs-captions-formats)":[
                     {
                        "[Format](#list-jobs-by-status-request-outputs-captions-captionformat)":"cea-708|dfxp|mov-text|scc|srt|webvtt",
                        "[Pattern](#list-jobs-by-status-request-outputs-captions-pattern)":"myCaption/file-language",
                        "[Encryption](#list-jobs-by-status-response-output-encryption)":{
                           "[Mode](#list-jobs-by-status-response-output-encrypt-mode)":"s3|s3-aws-kms|aes-cbc-pkcs7|
                              aes-ctr|aes-gcm",
                           "[Key](#list-jobs-by-status-response-output-encrypt-key)":"encrypted and base64-encoded encryption 
                              key",
                           "[KeyMd5](#list-jobs-by-status-response-output-encrypt-key-md5)":"base64-encoded key digest",
                           "[InitializationVector](#list-jobs-by-status-response-output-encrypt-vector)":"base64-encoded 
                              initialization vector"
                        }
                     },
                     {...}
                  ]
               },
               "[AppliedColorSpaceConversion](#list-jobs-by-status-response-output-color-space)":"None|Bt601ToBt709|
                  Bt709ToBt601"
            },
            {...}
         ],
         "[Playlists](#list-jobs-by-status-response-playlists)":[
            {
               "[Format](#list-jobs-by-status-response-playlists-format)":"HLSv3|HLSv4|MPEG-DASH|Smooth",
               "[Name](#list-jobs-by-status-response-playlists-name)":"name", 
               "[OutputKeys](#list-jobs-by-status-response-playlists-output-keys)":[
                  "Outputs:Key to include in this playlist",
                  ...
               ],
               "[HlsContentProtection](#list-jobs-by-status-request-hls-cp)":{
                  "[Method](#list-jobs-by-status-request-hls-method)":"aes-128",
                  "[Key](#list-jobs-by-status-request-hls-key)":"encrypted and base64-encoded protection key",
                  "[KeyMd5](#list-jobs-by-status-request-hls-key-md5)":"base64-encoded key digest",
                  "[InitializationVector](#list-jobs-by-status-request-hls-iv)":"base64-encoded
                        initialization vector",
                  "[LicenseAcquisitionUrl](#list-jobs-by-status-request-hls-url)":"license acquisition url",
                  "[KeyStoragePolicy](#list-jobs-by-status-request-hls-key-storage)":"NoStore|WithVariantPlaylists"
               },
               "[PlayReadyDrm](#list-jobs-by-status-response-drm)":{
                  "[Format](#list-jobs-by-status-response-drm-format)":"microsoft|discretix-3.0",
                  "[Key](#list-jobs-by-status-response-drm-key)":"encrypted and base64-encoded DRM key",
                  "[KeyId](#list-jobs-by-status-response-drm-key-id)":"id of the DRM key",
                  "[KeyMd5](#list-jobs-by-status-response-drm-key-md5)":"base64-encoded key digest",
                  "[InitializationVector](#list-jobs-by-status-response-drm-iv)":"base64-encoded
                        initialization vector",
                  "[LicenseAcquisitionUrl](#list-jobs-by-status-response-drm-url)":"license acquisition url"
               }
            },
            {...}
         ],
         "[UserMetadata](#list-jobs-by-status-response-outputs-user-metadata)":
            {
               "[Key](#list-jobs-by-status-response-outputs-metadata-key)":"[Value](#list-jobs-by-status-response-outputs-metadata-value)",
               "Second user metadata key":"Second user metadata value"
            },
         "[PipelineId](#list-jobs-by-status-response-pipeline-id)":"PipelineId for the job",
         "[Status](#list-jobs-by-status-response-job-status)":"Submitted|Progressing|Complete|Canceled|Error",
         "[Timing](#list-jobs-by-status-response-job-timing)":{
            "[SubmitTimeMillis](#list-jobs-by-status-response-job-timing-submit)":"job submitted time in epoch milliseconds",
            "[StartTimeMillis](#list-jobs-by-status-response-job-timing-start)":"job start time in epoch milliseconds",
            "[FinishTimeMillis](#list-jobs-by-status-response-job-timing-finish)":"job finish time in epoch milliseconds"
         }
      },
      {...}
   ],
   "[NextPageToken](#list-jobs-by-status-response-next-page-token)":value for accessing the next page of results|null
}
```

### Response Headers<a name="list-jobs-by-status-response-headers"></a>

This operation uses only response headers that are common to most responses\. For information about common response headers, see [HTTP Responses](making-http-requests.md#http-response-header)\.

### Response Body<a name="list-jobs-by-status-response-body"></a>

The response body contains one element for each job that satisfies the search criteria\. Each element contains the following JSON objects\.

**Id**  
The identifier that Elastic Transcoder assigned to the job\. You use this value to get settings for the job or to delete the job\.

**Inputs**  
Information about the file that Elastic Transcoder transcoded\. These are values that you specified when you created the job\.

**Inputs:Key**  
The name of the file that you want to transcode\. To determine which Amazon S3 bucket contains the specified file, Elastic Transcoder checks the pipeline specified by `PipelineId`; the `InputBucket` object in that pipeline identifies the bucket\.  
If the file name includes a prefix, for example, `cooking/lasagna.mpg`, include the prefix in the key\. If the file isn't in the specified bucket, Elastic Transcoder returns an error\.

**\(Optional\) Inputs:Encryption**  
The encryption settings, if any, that are used for decrypting your input files\. If your input file is encrypted, you must specify the mode that Elastic Transcoder will use to decrypt your file\.

**\(Required for Encryption\) Inputs:Encryption:Mode**  
The specific encryption mode that you want Elastic Transcoder to use when decrypting your files\.  
Elastic Transcoder supports the following options:  

+ **Amazon S3 Server\-Side Encryption:** Amazon S3 handles the encryption and decryption of your files\. As long as Elastic Transcoder has access permissions to your Amazon S3 bucket, you don't need to take any action\.

  For more information, see [Protecting Data Using Server\-Side Encryption](http://docs.aws.amazon.com/AmazonS3/latest/dev/serv-side-encryption.html) in the *Amazon Simple Storage Service Developer Guide*\.

+ **Client\-Side Encryption Using Customer\-Provided Keys:** Elastic Transcoder supports three types of encryption using customer\-provided keys:

  + **aes\-cbc\-pkcs7:** A padded cipher\-block mode of operation\.

  + **aes\-ctr:** AES Counter Mode\.

  + **aes\-gcm:** AES Galois Counter Mode, a mode of operation that is an authenticated encryption format, meaning that a file, key, or initialization vector that has been tampered with will fail the decryption process\.

  If you chose one of the AES\-encryption modes, you must also specify the following three values \(all three must be base64\-encoded\):

  + **Encryption Key**

  + **Encryption Key MD5**

  + **Encryption Initialization Vector**

**\(Optional\) Inputs:Encryption:Key**  
The data encryption key used to encrypt your file\. The key must be base64\-encoded and it must be one of the following bit lengths before being base64\-encoded:  
`128`, `192`, or `256`\.   
The key must also be encrypted by using AWS KMS\. For more information, see [Encrypting and Decrypting Data](http://docs.aws.amazon.com/kms/latest/developerguide/programming-encryption.html) in the *AWS Key Management Service Developer Guide*\.

**\(Optional\) Inputs:Encryption:KeyMd5**  
The MD5 digest of the key used to encrypt your input file, and that you want Elastic Transcoder to use as a checksum to make sure your key was not corrupted in transit\. The key MD5 must be base64\-encoded, and it must be exactly 16 bytes before being base64\-encoded\.

**\(Optional\) Inputs:Encryption:InitializationVector**  
The series of random bits created by a random bit generator, unique for every encryption operation, that you used to encrypt your input files\. The initialization vector must be base64\-encoded, and it must be exactly 16 bytes before being base64\-encoded\.  
For more information, go to [Initialization Vector](http://en.wikipedia.org/wiki/Initialization_vector)\.

**\(Optional\) Inputs:TimeSpan**  
Settings that determine when a clip begins and how long it lasts\.

**\(Optional\) Inputs:TimeSpan:StartTime**  
The place in the input file where you want a clip to start\. The format can be either HH:mm:ss\.SSS \(maximum value: 23:59:59\.999; SSS is thousandths of a second\) or sssss\.SSS \(maximum value: 86399\.999\)\. If you don't specify a value, Elastic Transcoder starts at the beginning of the input file\.

**\(Optional\) Inputs:TimeSpan:Duration**  
The duration of the clip\. The format can be either HH:mm:ss\.SSS \(maximum value: 23:59:59\.999; SSS is thousandths of a second\) or sssss\.SSS \(maximum value: 86399\.999\)\. If you don't specify a value, Elastic Transcoder creates an output file from StartTime to the end of the file\.  
If you specify a value longer than the duration of the input file , Elastic Transcoder transcodes the file and returns a warning message\.

**\(Optional\) Inputs:FrameRate**  
The frame rate of the input file\. If you want Elastic Transcoder to automatically detect the frame rate of the input file, specify `auto`\. If you want to specify the frame rate for the input file, enter one of the following values:   
`10`, `15`, `23.97`, `24`, `25`, `29.97`, `30`, `50`, `60`  
The default value is `auto`\.

**\(Optional\) Inputs:Resolution**  
The resolution, in pixels, of the input file\. This value must be `auto`, which causes Elastic Transcoder to automatically detect the resolution of the input file\.

**\(Optional\) Inputs:AspectRatio**  
The aspect ratio of the input file\. If you want Elastic Transcoder to automatically detect the aspect ratio of the input file, specify `auto`\. If you want to specify the aspect ratio for the output file, enter one of the following values:  
`1:1`, `4:3`, `3:2`, `16:9`  
The default value is `auto`\.

**\(Optional\) Inputs:Interlaced**  
Whether the input file is interlaced\. If you want Elastic Transcoder to automatically detect whether the input file is interlaced, specify `auto`\. If you want to specify whether the input file is interlaced, enter one of the following values:  
`true`, `false`  
The default value is `auto`\.

**\(Optional\) Inputs:Container**  
The container type for the input file\. If you want Elastic Transcoder to automatically detect the container type of the input file, specify `auto`\. If you want to specify the container type for the input file, enter one of the following values:  
`3gp`, `aac`, `asf`, `avi`, `divx`, `flv`, `m4a`, `mkv`, `mov`, `mp3`, `mp4`, `mpeg`, `mpeg-ps`, `mpeg-ts`, `mxf`, `ogg`, `vob`, `wav`, `webm`

**\(Automatic\) Inputs:DetectedProperties**  
The detected properties of the input file\. Elastic Transcoder identifies these values from the input file\.

**\(Automatic\) Inputs:Width**  
The detected width of the input file, in pixels\.

**\(Automatic\) Inputs:Height**  
The detected height of the input file, in pixels\.

**\(Automatic\) Inputs:FrameRate**  
The detected frame rate of the input file, in frames per second\.

**\(Automatic\) Inputs:FileSize**  
The detected file size of the input file, in bytes\.

**\(Automatic\) Inputs:DurationMillis**  
The detected duration of the input file, in milliseconds\.

**\(Video Only\) InputCaptions**  
You can configure Elastic Transcoder to transcode captions, or subtitles, from one format to another\. All captions must be in UTF\-8\. Elastic Transcoder supports two types of captions:  

+ **Embedded:** Embedded captions are included in the same file as the audio and video\. Elastic Transcoder supports only one embedded caption per language, to a maximum of 300 embedded captions per file\.

  Valid input values include `CEA-608 (EIA-608`, first non\-empty channel only\), `CEA-708 (EIA-708`, first non\-empty channel only\), and `mov-text`\.

  Valid outputs include mov\-text \(MP4 only\) and CEA\-708 \(MPEG\-TS and MP4, `29.97` and `30` frames per second only\)\. CEA\-708 captions are embedded in the H\.264 SEI user data of the stream\.

  Elastic Transcoder supports a maximum of one embedded format per output\.

+ **Sidecar:** Sidecar captions are kept in a separate metadata file from the audio and video data\. Sidecar captions require a player that is capable of understanding the relationship between the video file and the sidecar file\. Elastic Transcoder supports only one sidecar caption per language, to a maximum of 20 sidecar captions per file\.

  Valid input values include `dfxp` \(first div element only\), `ebu-tt`, `scc`, `smpt`, `srt`, `ttml` \(first div element only\), and `webvtt`\.

  Valid outputs include `dfxp` \(first div element only\), `scc`, `srt`, and `webvtt`\.
If you want ttml or smpte\-tt compatible captions, specify dfxp as your output format\.  
 Fmp4 containers with Smooth playlists support only dfxp, and Elastic Transcoder creates a file with the extension `.ismt`\. Fmp4 containers with MPEG\-DASH playlists support only webvtt, and Elastic Transcoder creates a file with the extension `.vtt`\.  
Elastic Transcoder does not support OCR \(Optical Character Recognition\), does not accept pictures as a valid input for captions, and is not available for audio\-only transcoding\. Elastic Transcoder does not preserve text formatting \(for example, italics\) during the transcoding process\.  
To remove captions or leave the captions empty, set `Captions` to null\. To pass through existing captions unchanged, set the `MergePolicy` to `MergeRetain`, and pass in a null `CaptionSources` array\.  
For more information about embedded files, see the [Subtitle \(caption\)](http://en.wikipedia.org/wiki/Subtitle_%28captioning%29#Creation.2C_delivery_and_display_of_subtitles) Wikipedia page\.  
For more information about sidecar files, see the [Metadata Platform](http://en.wikipedia.org/wiki/Extensible_Metadata_Platform) and [Sidecar file](http://en.wikipedia.org/wiki/Sidecar_file) Wikipedia pages\.

**\(Video Only\) InputCaptions:MergePolicy**  
A policy that determines how Elastic Transcoder handles the existence of multiple captions\.  

+ **MergeOverride:** Elastic Transcoder transcodes both embedded and sidecar captions into outputs\. If captions for a language are embedded in the input file and also appear in a sidecar file, Elastic Transcoder uses the sidecar captions and ignores the embedded captions for that language\.

+ **MergeRetain:** Elastic Transcoder transcodes both embedded and sidecar captions into outputs\. If captions for a language are embedded in the input file and also appear in a sidecar file, Elastic Transcoder uses the embedded captions and ignores the sidecar captions for that language\. If **CaptionSources** is empty, Elastic Transcoder omits all sidecar captions from the output files\.

+ **Override:** Elastic Transcoder transcodes only the sidecar captions that you specify in `CaptionSources`\.
`MergePolicy` cannot be null\.

**\(Video/Sidecar Only, Optional\) InputCaptions:CaptionSources**  
Source files for the input sidecar captions used during the transcoding process\. To omit all sidecar captions, leave `CaptionSources` blank\.

**\(Video Only\) InputCaptions:CaptionSources:Key**  
The name of the sidecar caption file that you want Elastic Transcoder to include with the outputs\.

**\(Video Only\) InputCaptions:CaptionSources:Language**  
A string that specifies the language of the caption\. Specify this as one of:  

+ 2\-character ISO 639\-1 code

+ 3\-character ISO 639\-2 code
For more information about ISO language codes, see [List of ISO 639\-1 codes](http://en.wikipedia.org/wiki/List_of_ISO_639-2_codes)\.

**\(Video Only, Optional\) InputCaptions:CaptionSources:TimeOffset**  
For clip generation or captions that do not start at the same time as the associated video file, the `TimeOffset` tells Elastic Transcoder how much of the video to encode before including captions\.  
Specify the TimeOffset in the form \[\+\-\]SS\.sss or \[\+\-\]HH:mm:SS\.ss\.

**\(Video Only, Optional\) InputCaptions:CaptionSources:Label**  
The label of the caption shown in the player when choosing a language\. We recommend that you put the caption language name here, in the language of the captions\.

**OutputKeyPrefix**  
The value, if any, that you want Elastic Transcoder to prepend to the names of all files that this job creates, including output files, thumbnails, and playlists\. If you specify a value, it must contain a `/` somewhere after the first character, which simplifies Amazon S3 file management\.

**Outputs**  
Information about the output files\. You can create a maximum of 30 outputs per job\. If you specify more than one output for a job, Elastic Transcoder creates the files for each output in the order in which you specify them in the job\. The `Outputs:Id` object identifies the position of an output in the sequence\.  
Each container type can hold the following output types\.      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-jobs-by-status.html)
In early versions of Elastic Transcoder, you could create just one output per job, so the object name was `Output`\. The `Output` syntax still works, but we recommend that you use the `Outputs` syntax for all jobs, even when you want Elastic Transcoder to transcode a file into only one format\. Do not use both the `Outputs` and `Output` syntaxes in the same request\.

**Outputs:Id**  
A sequential counter, starting with 1, that identifies an output among the outputs from the current job\. In the `Output` syntax, this value is always `1`\.

**Outputs:Key**  
The name that you want Elastic Transcoder to assign to the transcoded file and playlist\. Elastic Transcoder saves the file or files in the Amazon S3 bucket specified by the `OutputBucket` object in the pipeline that you specify in `PipelineId`\.  
If the bucket already contains a file that has the specified name, the output fails\. In the `Create Job` response, the value of `Outputs:Status` for that output will be `Error`, as will the final value of Status for the job\. However, other outputs in the same job may succeed\.  
The format for file names depends the container type and whether the segment duration is set\. If the container type is not `ts` or the segment duration is not provided, the name of the output file is a concatenation of `OutputKeyPrefix` and `Key`\.  
If the container type is `ts` and segment duration is provided, Elastic Transcoder uses the value of `Key` to name both the playlist for the output and the `.ts` files:  

+ **Playlist:**

  + **HLSv3:** The file name is a concatenation of `OutputKeyPrefix` and `Key` plus the file name extension `.m3u8`:

    *OutputKeyPrefix*`Key`*\.m3u8*

  + **HLSv4:** The file name is a concatenation of `OutputKeyPrefix` and `Key` plus the file name extension `_v4.m3u8`\. Video outputs create a second file with a file name that is a concatenation of `OutputKeyPrefix` and `Key` plus the file name extension `_iframe.m3u8`:

    *OutputKeyPrefix*`Key`*\_v4\.m3u8*

    *OutputKeyPrefix*`Key`*\_iframe\.m3u8*

+ **Segment \(\.ts\) files:**

  + **HLSv3:** The file name is a concatenation of `OutputKeyPrefix` and `Key`, plus a five\-digit sequential counter beginning with `00000`, and the file name extension `.ts`:

    *OutputKeyPrefix*`Key`*00000\.ts*

  + **HLSv4:** The file name is a concatenation of `OutputKeyPrefix` and `Key` plus the file name extension `.ts`:

    *OutputKeyPrefix*`Key`*\.ts*
If the container type is `ts` and a segmented ts output is not included in a master playlist, Elastic Transcoder treats the output as `HLSv3`\.  
Elastic Transcoder automatically appends the relevant file extension to outputs in an `HLSv3` or `HLSv4` playlist\. If you include a file extension in the `Outputs:Key` for `HLSv3` or `HLSv4` playlist outputs, the filename will have two extensions\.
`OutputKeyPrefix` groups all of the files for a job together in your Amazon S3 bucket\. If you want to group the files for each output within a job, you can include a prefix in the value of `Key`, for example:  
*OutputKeyPrefix*`iPhone/Key`*00000\.ts*  
*OutputKeyPrefix*`KindleFireHD/Key`*00000\.ts*

**\(Optional\) Outputs:Encryption**  
The encryption settings, if any, that you want Elastic Transcoder to apply to your output files\. If you choose to use encryption, you must specify a mode to use\. If you choose not to use encryption, Elastic Transcoder will write an unencrypted file to your Amazon S3 bucket\.

**\(Required for Encryption\) Outputs:Encryption:Mode**  
The specific encryption mode that you want Elastic Transcoder to use when encrypting your output files individually\. Elastic Transcoder supports the following **Encryption Mode** options:  

+ **s3:** Amazon S3 creates and manages the keys used for encrypting your files\.

  For more information, see [Protecting Data Using Server\-Side Encryption](http://docs.aws.amazon.com/AmazonS3/latest/dev/serv-side-encryption.html) in the *Amazon Simple Storage Service Developer Guide*\.

+ **s3\-aws\-kms:** Amazon S3 calls AWS KMS, which creates and manages the keys that are used for encrypting your files\. If you specify **s3\-aws\-kms** and you don't want to use the default key, you must add the AWS\-KMS key that you want to use to your pipeline\.

  For more information, see [Protecting Data Using Server\-Side Encryption with AWS KMS\-Managed Keys ](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html) in the *Amazon Simple Storage Service Developer Guide*\.

+ **aes\-cbc\-pkcs7:** A padded cipher\-block mode of operation\.

+ **aes\-ctr:** AES Counter Mode\.

+ **aes\-gcm:** AES Galois Counter Mode, a mode of operation that is an authenticated encryption format, meaning that a file, key, or initialization vector that has been tampered with will fail the decryption process\.
If you chose one of the AES\-encryption modes, you must also specify the following three values \(all three must be base64\-encoded\):  

+ **Encryption Key**

+ **Encryption Key MD5**

+ **Encryption Initialization Vector**
If you chose one of the AES\-encryption modes, and you want Elastic Transcoder to generate a `128`\-bit AES encryption key for you, do not specify values for the **Encryption Key**, **Encryption Key MD5**, or **Encryption Initialization Vector**\. Once Elastic Transcoder has generated the key, you can retrieve the key by calling `ReadJob`\. The key is not included in the `CreateJobResponse` object\.  
For the AES modes, your media\-specific private encryption keys and your unencrypted data are never stored by AWS; therefore, it is important that you safely manage your encryption keys\. If you lose them, you won't be able to decrypt your data\.

**\(Optional\) Outputs:Encryption:Key**  
If you want Elastic Transcoder to generate a key for you, leave this field blank\. Once Elastic Transcoder has generated the key, you can retrieve the key by calling `ReadJob`\. The key is not included in the `CreateJobResponse` object\.  
If you choose to supply your own key, you must encrypt the key by using AWS KMS\. The key must be base64\-encoded, and it must be one of the following bit lengths before being base64\-encoded:  
`128`, `192`, or `256`\.   
If you configured Elastic Transcoder to generate a key for you, Elastic Transcoder leaves this field blank in the `CreateJob` response\. To retrieve your generated data encryption key, submit a `ReadJob` request\.  
For more information about encrypting your key with AWS KMS, see [Encrypting and Decrypting Data](http://docs.aws.amazon.com/kms/latest/developerguide/programming-encryption.html) in the *AWS Key Management Service Developer Guide*\.

**\(Optional\) Outputs:Encryption:KeyMd5**  
The MD5 digest of the key that you want Elastic Transcoder to use to encrypt your output file, and that you want Elastic Transcoder to use as a checksum to make sure your key was not corrupted in transit\. The key MD5 must be base64\-encoded, and it must be exactly 16 bytes before being base64\-encoded\.  
If Elastic Transcoder is generating your key for you, you must leave this field blank\.

**\(Optional\) Outputs:Encryption:InitializationVector**  
The series of random bits created by a random bit generator, unique for every encryption operation, that you want Elastic Transcoder to use to encrypt your output files\. The initialization vector must be base64\-encoded, and it must be exactly 16 bytes before being base64\-encoded\.  
If Elastic Transcoder is generating your key for you, you must leave this field blank\.  
For more information, go to [Initialization Vector](http://en.wikipedia.org/wiki/Initialization_vector)\.

**\(Optional\) Outputs:ThumbnailPattern**  
Whether you want Elastic Transcoder to create thumbnails for your videos and, if so, how you want Elastic Transcoder to name the files\.  
If you don't want Elastic Transcoder to create thumbnails, specify `""`\.  
If you do want Elastic Transcoder to create thumbnails, specify the information that you want to include in the file name for each thumbnail\. You can specify the following values in any sequence:  

+ **`{count}` \(Required\):** If you want to create thumbnails, you must include `{count}` in the `ThumbnailPattern` object\. Wherever you specify `{count}`, Elastic Transcoder adds a five\-digit sequence number \(beginning with **00001**\) to thumbnail file names\. The number indicates where a given thumbnail appears in the sequence of thumbnails for a transcoded file\. 
**Important**  
If you specify a literal value and/or `{resolution}` but you omit `{count}`, Elastic Transcoder returns a validation error and does not create the job\.

+ **\(Optional\) Literal values:** You can specify literal values anywhere in the `ThumbnailPattern` object, for example, as a file name prefix or as a delimiter between `{resolution}` and `{count}`\.

+ **\(Optional\) `{resolution}`:** If you want Elastic Transcoder to include the resolution in the file name, include `{resolution}` in the `ThumbnailPattern` object\. 
When creating thumbnails, Elastic Transcoder automatically saves the files in the format \(`.jpg` or `.png`\) that appears in the preset that you specified in `PresetId`\. Elastic Transcoder also appends the applicable file name extension\.  
As with `Outputs:Key`, you can include a prefix in `ThumbnailPattern` that groups the applicable files together, for example, all of the thumbnails for one video in one format, or all of the thumbnails with the corresponding output file\.

**\(Optional\) Outputs:Rotate**  
The number of degrees clockwise by which you want Elastic Transcoder to rotate the output relative to the input\. The following values are valid:  
`auto`, `0`, `90`, `180`, `270`  
The value `auto` generally works only if the file that you're transcoding contains rotation metadata\. 

**Outputs:PresetId**  
The value of the `Id` object for the preset that you want to use for this job\. The preset determines the audio, video, and thumbnail settings that Elastic Transcoder uses for transcoding\. To use a preset that you created, specify the preset ID that Elastic Transcoder returned in the response when you created the preset\.  
If you created any presets before AAC profiles were added, Elastic Transcoder uses the AAC\-LC profile for those presets\.
For a list of system presets, see [System Presets](system-presets.md) \(You can also get these IDs using [List Presets](list-presets.md)\.\)

**\(Fragmented MP4/MPEG\-TS Outputs Only\) Outputs:SegmentDuration**  
If you specify a preset for the current output for which the value of `Container` is either **ts** \(MPEG\-TS\) or **fmp4** \(Fragmented MP4\), `SegmentDuration` is the target maximum duration of each segment in seconds\. For `HLSv3` format playlists, each media segment is stored in a separate `.ts` file\. For `HLSv4`, `MPEG-DASH`, and `Smooth` playlists, all media segments for an output are stored in a single file\. Each segment is approximately the length of the `SegmentDuration`, though individual segments might be shorter or longer\.   
The range of valid values is 1 to 60 seconds\. If the duration of the video is not evenly divisible by `SegmentDuration`, the duration of the last segment is the remainder of:  
`total length/SegmentDuration`  
Elastic Transcoder creates an output\-specific playlist for each `HLS` output that you specify in `OutputKeys`\. To add an output to a master playlist for this job, include it in [Outputs in Master Playlist](job-settings.md#job-settings-playlist-outputs)\.  
Elastic Transcoder applies this segmenting to any captions associated with the output video\.  
For more information, see [HTTP Live Streaming](http://en.wikipedia.org/wiki/HTTP_Live_Streaming)\.

**\(Video Only\) Outputs:Watermarks**  
Information about the watermarks that you want Elastic Transcoder to add to the video or artwork during transcoding\. You can specify up to four watermarks for each output\. Settings for each watermark must be defined in the preset that you specify in `Outputs:PresetId` for the current output\.  
Watermarks are added to the output file in the sequence in which you list them in the job output—the first watermark in the list is added to the output file first, the second watermark in the list is added next, and so on\. As a result, if the settings in a preset cause Elastic Transcoder to place all watermarks in the same location, the second watermark that you list in `Outputs:Watermarks` will cover the first one, the third one will cover the second, and the fourth one will cover the third\.  
For more information about watermarks, see [Watermarks](watermarks.md)\.

**\(Video Only\) Outputs:Watermarks:InputKey**  
The name of the `.png` or `.jpg` file that you want to use for the watermark\. To determine which Amazon S3 bucket contains the specified file, Elastic Transcoder checks the pipeline specified by `PipelineId`; the `InputBucket` object in that pipeline identifies the bucket\.  
If the file name includes a prefix, for example, `logos/128x64.png`, include the prefix in the key\. If the file isn't in the specified bucket, Elastic Transcoder returns an error\.

**\(Video Only\) Outputs:Watermarks:PresetWatermarkId**  
The ID of the watermark settings that Elastic Transcoder uses to add watermarks to the file during transcoding\. The settings are in the preset specified by `Outputs:PresetId` for the current output\. In that preset, the value of `Watermarks:Id` tells Elastic Transcoder which settings to use\. 

**\(FLAC/MP3/MP4 Only\) Outputs:AlbumArt**  
The album art to be associated with the output file, if any\.  
To remove artwork or leave the artwork empty, you can either set `Artwork` to null, or set the `MergePolicy` to `Replace` and use an empty `Artwork` array\.  
To pass through existing artwork unchanged, set the `MergePolicy` to `Prepend`, `Append`, or `Fallback`, and use an empty `Artwork` array\.  
Album Art is available only for containers of type `mp3` or `mp4`\.

**\(FLAC/MP3/MP4 Only\) Outputs:AlbumArt:MergePolicy **  
A policy that determines how Elastic Transcoder handles the existence of multiple album artwork files\.  

+ **Replace:** The specified album art replaces any existing album art\.

+ **Prepend:** The specified album art is placed in front of any existing album art\.

+ **Append:** The specified album art is placed after any existing album art\. 

+ **Fallback:** If the input file contains artwork, Elastic Transcoder uses that artwork for the output\. If the input does not contain artwork, Elastic Transcoder uses the specified album art file\.

**\(FLAC/MP3/MP4 Only\) Outputs:AlbumArt:Artwork**  
The file to be used as album art\. There can be multiple artworks associated with an audio file, to a maximum of 20\.

**\(FLAC/MP3/MP4 Only\) Outputs:AlbumArt:Artwork:InputKey**  
The name of the file to be used as album art\. To determine which Amazon S3 bucket contains the specified file, Elastic Transcoder checks the pipeline specified by `PipelineId`; the `InputBucket` object in that pipeline identifies the bucket\.  
If the file name includes a prefix, for example, `cooking/pie.jpg`, include the prefix in the key\. If the file isn't in the specified bucket, Elastic Transcoder returns an error\.

**\(FLAC/MP3/MP4 Only\) Outputs:AlbumArt:Artwork:MaxWidth**  
The maximum width of the output album art in pixels\. If you specify `auto`, Elastic Transcoder uses 600 as the default value\. If you specify a numeric value, enter an even integer between 32 and 4096, inclusive\.

**\(FLAC/MP3/MP4 Only\) Outputs:AlbumArt:Artwork:MaxHeight**  
The maximum height of the output album art in pixels\. If you specify `auto`, Elastic Transcoder uses 600 as the default value\. If you specify a numeric value, enter an even integer between 32 and 3072, inclusive\.

**\(FLAC/MP3/MP4 Only\) Outputs:AlbumArt:Artwork:SizingPolicy**  
A value that controls scaling of the output album art:  

+ **Fit:** Elastic Transcoder scales the output art so it matches the value that you specified in either `MaxWidth` or `MaxHeight` without exceeding the other value\.

+ **Fill:** Elastic Transcoder scales the output art so it matches the value that you specified in either `MaxWidth` or `MaxHeight` and matches or exceeds the other value\. Elastic Transcoder centers the output art and then crops it to the dimension \(if any\) that exceeds the maximum value\. 

+ **Stretch:** Elastic Transcoder stretches the output art to match the values that you specified for `MaxWidth` and `MaxHeight`\. If the relative proportions of the input art and the output art are different, the output art will be distorted\.

+ **Keep:** Elastic Transcoder does not scale the output art\. If either dimension of the input art exceeds the values that you specified for `MaxWidth` and `MaxHeight`, Elastic Transcoder crops the output art\.

+ **ShrinkToFit:** Elastic Transcoder scales the output art down so that its dimensions match the values that you specified for at least one of `MaxWidth` and `MaxHeight` without exceeding either value\. If you specify this option, Elastic Transcoder does not scale the art up\.

+ **ShrinkToFill:** Elastic Transcoder scales the output art down so that its dimensions match the values that you specified for at least one of `MaxWidth` and `MaxHeight` without dropping below either value\. If you specify this option, Elastic Transcoder does not scale the art up\.
The following table shows possible effects of `SizingPolicy` settings on the output album art:      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-jobs-by-status.html)

**\(FLAC/MP3/MP4 Only\) Outputs:AlbumArt:Artwork:PaddingPolicy**  
When you set `PaddingPolicy` to `Pad`, Elastic Transcoder might add white bars to the top and bottom and/or left and right sides of the output album art to make the total size of the output art match the values that you specified for `MaxWidth` and `MaxHeight`\. For more information, see the table at `AlbumArt:Art:SizingPolicy`\.

**\(FLAC/MP3/MP4 Only\) Outputs:AlbumArt:Artwork:AlbumArtFormat**  
The format of album art, if any\. Valid formats are `jpg` and `png`\. 

**Outputs:Duration**  
Duration of the output file in seconds, rounded up\.

**Outputs:DurationMillis**  
Duration of the output file, in milliseconds\.

**Outputs:Width**  
Width of the output file, in pixels\.

**Outputs:Height**  
Height of the output file, in pixels\.

**Outputs:FrameRate**  
Frame rate of the output file, in frames per second\.

**Outputs:FileSize**  
File size of the output file, in bytes\.

**Outputs:Status**  
The status of one output in a job\. If you specified only one output for the job, `Outputs:Status` is always the same as `Job:Status`\. If you specified more than one output:  

+ `Job:Status` and `Outputs:Status` for all of the outputs is `Submitted` until Elastic Transcoder starts to process the first output\.

+ When Elastic Transcoder starts to process the first output, `Outputs:Status` for that output and `Job:Status` both change to `Progressing`\. For each output, the value of `Outputs:Status` remains `Submitted` until Elastic Transcoder starts to process the output\.

+ `Job:Status` remains `Progressing` until all of the outputs reach a terminal status, either `Complete` or `Error`\.

+ When all of the outputs reach a terminal status, `Job:Status` changes to `Complete` only if `Outputs:Status` for all of the outputs is `Complete`\. If `Outputs:Status` for one or more outputs is `Error`, the terminal status for `Job:Status` is also `Error`\.
The value of `Status` is one of the following: `Submitted`, `Progressing`, `Complete`, `Canceled`, or `Error`\.

**Outputs:StatusDetail**  
Information that further explains `Outputs:Status`\.

**\(Video Only\) Outputs:Captions**  
You can configure Elastic Transcoder to transcode captions, or subtitles, from one format to another\. All captions must be in UTF\-8\. Elastic Transcoder supports two types of captions:  

+ **Embedded:** Embedded captions are included in the same file as the audio and video\. Elastic Transcoder supports only one embedded caption per language, to a maximum of 300 embedded captions per file\.

  Valid input values include `CEA-608 (EIA-608`, first non\-empty channel only\), `CEA-708 (EIA-708`, first non\-empty channel only\), and `mov-text`\.

  Valid outputs include mov\-text \(MP4 only\) and CEA\-708 \(MPEG\-TS and MP4, `29.97` and `30` frames per second only\)\. CEA\-708 captions are embedded in the H\.264 SEI user data of the stream\.

  Elastic Transcoder supports a maximum of one embedded format per output\.

+ **Sidecar:** Sidecar captions are kept in a separate metadata file from the audio and video data\. Sidecar captions require a player that is capable of understanding the relationship between the video file and the sidecar file\. Elastic Transcoder supports only one sidecar caption per language, to a maximum of 20 sidecar captions per file\.

  Valid input values include `dfxp` \(first div element only\), `ebu-tt`, `scc`, `smpt`, `srt`, `ttml` \(first div element only\), and `webvtt`\.

  Valid outputs include `dfxp` \(first div element only\), `scc`, `srt`, and `webvtt`\.
If you want ttml or smpte\-tt compatible captions, specify dfxp as your output format\.  
 Fmp4 containers with Smooth playlists support only dfxp, and Elastic Transcoder creates a file with the extension `.ismt`\. Fmp4 containers with MPEG\-DASH playlists support only webvtt, and Elastic Transcoder creates a file with the extension `.vtt`\.  
Elastic Transcoder does not support OCR \(Optical Character Recognition\), does not accept pictures as a valid input for captions, and is not available for audio\-only transcoding\. Elastic Transcoder does not preserve text formatting \(for example, italics\) during the transcoding process\.  
To remove captions or leave the captions empty, set `Captions` to null\. To pass through existing captions unchanged, set the `MergePolicy` to `MergeRetain`, and pass in a null `CaptionSources` array\.  
For more information about embedded files, see the [Subtitle \(caption\)](http://en.wikipedia.org/wiki/Subtitle_%28captioning%29#Creation.2C_delivery_and_display_of_subtitles) Wikipedia page\.  
For more information about sidecar files, see the [Metadata Platform](http://en.wikipedia.org/wiki/Extensible_Metadata_Platform) and [Sidecar file](http://en.wikipedia.org/wiki/Sidecar_file) Wikipedia pages\.

**\(Video Only\) Outputs:Captions:CaptionFormats**  
The file format of the output captions\. If you leave this value blank, Elastic Transcoder returns an error\.

**\(Video Only\) Outputs:Captions:CaptionFormats:Format**  
The format you specify determines whether Elastic Transcoder generates an embedded or sidecar caption for this output\.  

+ **Embedded Caption Formats:**    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-jobs-by-status.html)

  Elastic Transcoder supports a maximum of one embedded format per output\.

+ **Sidecar Caption Formats:** Elastic Transcoder supports dfxp \(first div element only\), scc, srt, and webvtt\. If you want ttml or smpte\-tt compatible captions, specify dfxp as your output format\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-jobs-by-status.html)
`fmp4` captions have an extension of `.ismt` \(dfxp\) or `.vtt` \(webvtt\)\.

**\(Video/Sidecar Only\) Outputs:Captions:CaptionFormats:Pattern**  
The prefix for caption filenames, in the form *description*\-`{language}`, where:  

+ *description* is a description of the video\.

+ `{language}` is a literal value that Elastic Transcoder replaces with the two\- or three\-letter code for the language of the caption in the output file names\.
If you don't include `{language}` in the file name pattern, Elastic Transcoder automatically appends "`{language}`" to the value that you specify for the description\. In addition, Elastic Transcoder automatically appends the count to the end of the segment files\.  
For example, suppose you're transcoding into srt format\. When you enter "Sydney\-\{language\}\-sunrise", and the language of the captions is English \(en\), the name of the first caption file will be `Sydney-en-sunrise00000.srt`\.

**\(Automatic\) Outputs:AppliedColorSpaceConversion**  
If Elastic Transcoder used a preset with a `ColorSpaceConversionMode` to transcode the output file, the `AppliedColorSpaceConversion` parameter shows the conversion used\. If no `ColorSpaceConversionMode` was defined in the preset, this parameter will not be included in the job response\.  
For more information about `ColorSpaceConversionMode`, see [ColorSpaceConversion](create-preset.md#create-preset-request-video-color-space)\.

**\(Optional\) Outputs:UserMetadata**  
User\-defined metadata that you want to associate with an Elastic Transcoder job\.  You specify metadata in `key/value` pairs\. You can use the `key/value` pairs to track details about a file, for example, `Season 1: Episode 3`\.  
You can add up to 10 key/value pairs to each job\. Elastic Transcoder does not guarantee that `key/value` pairs are returned in the same order in which you specify them\.

**Outputs:UserMetadata:Key**  
The key of the metadata `key/value` pair that you want returned with the output file\. Each key must be a unique string between `1-128` characters, and must use only characters from the following list:  

+ `0-9`

+ `A-Z` and `a-z`

+ `Space`

+ The following symbols: `_.:/=+-%@`
You can use keys as a numbering system for organizing your metadata, for storing an extra 128 characters of metadata, or for labeling the metadata stored in the **value**\. If you want to use only value metadata, you can put throw\-away strings in your keys such as `key1`, and ignore the keys when you retrieve your metadata from Elastic Transcoder\.   
You must specify unique strings for all of the keys in a job\. If the same string is used for more than one key in a job, Elastic Transcoder returns only one of the key/value pairs that use that key\. There is no way to guarantee which value is returned\.

**Outputs:UserMetadata:Value**  
The value of the metadata `key/value` pair that you want returned with your job\. Each value must be a string between `0-256` characters, and must use only characters from the following list:   

+ `0-9`

+ `A-Z` and `a-z`

+ `Space`

+ The following symbols: `_.:/=+-%@`

**\(Fragmented MP4/MPEG\-TS Outputs Only\) Playlists**  
If you specify a preset in `PresetId` for which the value of `Container` is either **ts** \(MPEG\-TS\) or **fmp4** \(Fragmented MP4\), `Playlists` contains information about the master playlists that you want Elastic Transcoder to create\.  
We recommend that you create at most one master playlist per playlist format\. The maximum number of master playlists in a job is 30\.

**Playlists:Format**  
The format of the output playlist\. Valid formats are `HLSv3`, `HLSv4`, `MPEG-DASH`, and `Smooth`\.

**Playlists:Name**  
The name that you want Elastic Transcoder to assign to a master playlist, for example, `nyc-vacation.m3u8`\. If the name includes a `/` character, the section of the name before the `/` must be identical for all `Name` objects\. If you create more than one master playlist, the values of all `Name` objects must be unique\.  
Elastic Transcoder automatically appends the relevant file extension to the file name \(`.m3u8` for `HLSv3` and `HLSv4` playlists, `.mpd` for `MPEG-DASH` playlists, and `.ism` and `.ismc` for `Smooth` playlists\)\. If you include a file extension in `MasterPlaylistName`, the file name will have two extensions\.
Any segment duration settings, clip settings, or caption settings must be the same for all outputs in the playlist\. For `Smooth` playlists, the `Audio:Profile`, `Video:Profile`, and `Video:FrameRate` to `Video:KeyframesMaxDist` ratio must be the same for all outputs\. For more information, see [KeyframesMaxDist](create-preset.md#create-preset-request-video-key-frames-max-dist)\.

**Playlists:OutputKeys**  
For each output in this job that you want to include in a master playlist, the value of the `Outputs:Key` object\. If you include more than one output in a playlist, the value of `SegmentDuration` for all of the outputs must be the same\.   
For `HLSv4` master playlists, Elastic Transcoder chooses which combinations of audio and video inputs will be linked in the output playlists\. The first audio and video inputs will be linked and rendered as the default playback experience, allowing you to choose your preferred playback default\. For other individual playlists in the master playlist, Elastic Transcoder chooses which audio and video bit rate combinations will provide the best playback\.

**\(Optional\) Playlists:HlsContentProtection**  
The HLS content protection settings, if any, that you want Elastic Transcoder to apply to your output files\. If you want to use HLS content protection do not specify encryption settings for the output file or captions\. HLS content protection encrypts each segment of a file so that they can be streamed encrypted and only decrypted on playback, while the output file and caption encryptions encrypt the file all at once\. Elastic Transcoder does not support files that are encrypted both ways\.

**Playlists:HlsContentProtection:Method**  
The content protection method for your output\. The only valid value is:  
`aes-128`\.  
This value will be written into the `method` attribute of the `EXT-X-KEY` metadata tag in the output playlist\.

**\(Optional\) Playlists:HlsContentProtection:Key**  
If you want Elastic Transcoder to generate a key for you, leave this field blank\. Once Elastic Transcoder has generated the key, you can retrieve the key by calling `ReadJob`\. The key is not included in the `CreateJobResponse` object\.  
If you choose to supply your own key, you must encrypt the key by using AWS KMS\. The key must be base64\-encoded, and it must be one of the following bit lengths before being base64\-encoded:  
`128`, `192`, or `256`\.   
If you configured Elastic Transcoder to generate a key for you, Elastic Transcoder leaves this field blank in the `CreateJob` response\. To retrieve your generated data encryption key, submit a `ReadJob` request\.  
For more information about encrypting your key with AWS KMS, see [Encrypting and Decrypting Data](http://docs.aws.amazon.com/kms/latest/developerguide/programming-encryption.html) in the *AWS Key Management Service Developer Guide*\.

**\(Optional\) Playlists:HlsContentProtection:KeyMd5**  
The MD5 digest of the key that you want Elastic Transcoder to use to encrypt your output file, and that you want Elastic Transcoder to use as a checksum to make sure your key was not corrupted in transit\. The key MD5 must be base64\-encoded, and it must be exactly 16 bytes before being base64\-encoded\.  
If Elastic Transcoder is generating your key for you, you must leave this field blank\.

**\(Optional\) Playlists:HlsContentProtection:InitializationVector**  
The series of random bits created by a random bit generator, unique for every encryption operation, that you want Elastic Transcoder to use to encrypt your output files\. The initialization vector must be base64\-encoded, and it must be exactly 16 bytes before being base64\-encoded\.  
If Elastic Transcoder is generating your key for you, you must leave this field blank\.  
For more information, go to [Initialization Vector](http://en.wikipedia.org/wiki/Initialization_vector)\.

**Playlists:HlsContentProtection:LicenseAcquisitionUrl**  
The location of the license key required to decrypt your HLS playlist\. The URL must be an absolute path, and is referenced in the URI attribute of the EXT\-X\-KEY metadata tag in the playlist file\. For example:  

```
https://www.example.com/exampleKey/
```

**Playlists:HlsContentProtection:KeyStoragePolicy**  
Specify whether you want Elastic Transcoder to write your HLS license key to an Amazon S3 bucket\. If you choose `WithVariantPlaylists`, Elastic Transcoder will write your encrypted key into the same Amazon S3 bucket as the associated playlist\.  
If you chose `NoStore`, Elastic Transcoder will not store your key\. You are responsible for storing it and providing it to your users by giving them the **License Acquisition URL** where you are storing the key\.

** \(Optional\) Playlists:PlayReadyDrm**  
The DRM settings used to restrict who can watch your files\. This is done by including a PlayReady DRM header in your output playlist\. This is not usable for artwork, captions, thumbnails, or watermarks\. PlayReady DRM encrypts your media files using `aes-ctr` encryption\.  
If you use DRM for an `HLSv3` playlist, your outputs must have a master playlist\.  
For more information, see [Digital Rights Management](drm.md)\.

** Playlists:PlayReadyDrm:Format**  
The DRM format for your output playlist\. Valid formats are `discretix-3.0` and `microsoft`\.  
For playlists of type `Smooth`, specify `microsoft`\. For playlists of type `HLSv3`, specify `discretix-3.0`\.

**Playlists:PlayReadyDrm:Key**  
The DRM key for your file, provided by your DRM license provider\. The key must be base64\-encoded, and it must be one of the following bit lengths before being base64\-encoded:  
`128`, `192`, or `256`\.   
The key must also be encrypted by using AWS KMS\. For more information, see [Encrypting and Decrypting Data](http://docs.aws.amazon.com/kms/latest/developerguide/programming-encryption.html) in the *AWS Key Management Service Developer Guide*\.

**Playlists:PlayReadyDrm:KeyId**  
The ID for your DRM key, so that your DRM license provider knows which key to provide\.  
The key ID must be provided in big endian, and Elastic Transcoder will convert it to little endian before inserting it into the PlayReady DRM headers\. If you are unsure whether your license server provides your key ID in big or little endian, check with your DRM provider\.

**Playlists:PlayReadyDrm:KeyMd5**  
The MD5 digest of the key used for DRM on your file, and that you want Elastic Transcoder to use as a checksum to make sure your key was not corrupted in transit\. The key MD5 must be base64\-encoded, and it must be exactly 16 bytes before being base64\-encoded\.

** \(Optional\) Playlists:PlayReadyDrm:InitializationVector**  
The series of random bits created by a random bit generator, unique for every encryption operation, that you want Elastic Transcoder to use to encrypt your files\. The initialization vector must be base64\-encoded, and it must be exactly 8 bytes long before being base64\-encoded\. If no initialization vector is provided, Elastic Transcoder generates one for you\.  
For more information, go to [Initialization Vector](http://en.wikipedia.org/wiki/Initialization_vector)\.

**Playlists:PlayReadyDrm:LicenseAcquisitionUrl**  
The location of the license key required to play DRM content\. The URL must be an absolute path, and is referenced by the PlayReady header\. The PlayReady header is referenced in the protection header of the client manifest for Smooth Streaming outputs, and in the EXT\-X\-DXDRM and EXT\-XDXDRMINFO metadata tags for HLS playlist outputs\. An example URL looks like this:  

```
https://www.example.com/exampleKey/
```

**PipelineId**  
The value of the `Id` object for the pipeline that you want Elastic Transcoder to use for transcoding\. The pipeline determines several settings, including the Amazon S3 bucket from which Elastic Transcoder gets the files to transcode and the bucket into which Elastic Transcoder puts the transcoded files\.

**Status**  
If you specified more than one output for the job, the status of the entire job\. When Elastic Transcoder starts processing a job, the value of `Job:Status` changes to `Progressing` and doesn't change until Elastic Transcoder has finished processing all outputs\. When processing is complete, `Job:Status` changes either to `Complete` or, if any of the outputs failed, to `Error`\.  
If you specified only one output for the job, `Job:Status` is the same as `Outputs:Status`\.   
The value of `Job:Status` is one of the following: `Submitted`, `Progressing`, `Complete`, `Canceled`, or `Error`\.

**Timing**  
The details about the timing of a job\.

** Timing:SubmitTimeMillis**  
The time the job was submitted to Elastic Transcoder, in epoch milliseconds\.

** Timing:StartTimeMillis**  
The time the job began transcoding, in epoch milliseconds\.

** Timing:FinishTimeMillis**  
The time the job finished transcoding, in epoch milliseconds\.  
To learn more about epoch time, go to the [ Epoch Computing](https://en.wikipedia.org/wiki/Epoch_%28reference_date%29#Computing) page on Wikipedia\.

**NextPageToken**  
A value that you use to access the second and subsequent pages of results, if any\. When the jobs in the specified pipeline fit on one page or when you've reached the last page of results, the value of `NextPageToken` is `null`\.

## Errors<a name="list-jobs-by-status-response-errors"></a>

For information about Elastic Transcoder exceptions and error messages, see [Handling Errors in Elastic Transcoder](error-handling.md)\.

## Examples<a name="list-jobs-by-status-examples"></a>

The following example request creates a job\.

### Sample Request<a name="list-jobs-by-status-examples-sample-request"></a>

The following example request gets a list of all of the jobs that you have ever created that have a status of `Complete`\. 

```
GET /2012-09-25/jobsByStatus/Complete?Ascending=true HTTP/1.1
Content-Type: charset=UTF-8
Accept: */*
Host: elastictranscoder.Elastic Transcoder endpoint.amazonaws.com:443
x-amz-date: 20130114T174952Z
Authorization: AWS4-HMAC-SHA256
               Credential=AccessKeyID/request-date/Elastic Transcoder endpoint/elastictranscoder/aws4_request,
               SignedHeaders=host;x-amz-date;x-amz-target,
               Signature=calculated-signature
```

### Sample Response<a name="list-jobs-by-status-examples-sample-response"></a>

```
Status: 200 OK
x-amzn-RequestId: c321ec43-378e-11e2-8e4c-4d5b971203e9
Content-Type: application/json
Content-Length: number of characters in the response
Date: Mon, 14 Jan 2013 06:01:47 GMT

{
   "Jobs":[
      {
         "Id":"3333333333333-abcde3",
         "Input":[{
            "Key":"cooking/lasagna.mp4",
            "FrameRate":"auto",
            "Resolution":"auto",
            "AspectRatio":"auto",
            "Interlaced":"auto",
            "Container":"mp4",
            "InputCaptions"{
               "MergePolicy":"MergeOverride",
               "CaptionSources":[
                  {
                     "Key":"scc/lasagna-kindlefirehd.scc",
                     "Language":"en",
                     "Label":"English"
                  },
                  {
                     "Key":"srt/lasagna-kindlefirehd.srt",
                     "Language":"fr",
                     "TimeOffset":"1:00:00",
                     "Label":"French"
                  }
               ]
            },
            "DetectedProperties":{
               "Width":"1280",
               "Height":"720",
               "FrameRate":"30.00",
               "FileSize":"5872000",
               "DurationMillis":"1003000"
            }
         }],
         "OutputKeyPrefix":"",
         "Outputs":[
            {
               "Id":"1",
               "Key":"mp4/lasagna-kindlefirehd.mp4",
               "ThumbnailPattern":"mp4/thumbnails/lasagna-{count}",
               "Rotate":"0",
               "PresetId":"1351620000000-100080",
               "Watermarks":[
                  {
                     "InputKey":"logo/128x64.png",
                     "PresetWatermarkId":"company logo 128x64",
                  }
               ],
               "Duration":"1003",
               "DurationMillis":"1003000",
               "Width":"1280",
               "Height":"720",
               "FrameRate":"30.00",
               "FileSize":"5872000",
               "Status":"Complete",
               "StatusDetail":"",
               "Captions":{
                  "CaptionFormats":[
                     {
                        "Format":"scc",
                        "Pattern":"scc/lasagna-{language}"
                     },
                     {
                        "Format":"srt",
                        "Pattern":"srt/lasagna-{language}"
                     },
                     {
                        "Format":"mov-text"
                     }
                  ]
               },
               "AppliedColorSpaceConversion":"None"
            },
            {
               "Id":"2",
               "Key":"iphone/lasagna-1024k",
               "ThumbnailPattern":"iphone/th1024k/lasagna-{count}",
               "Rotate":"0",
               "PresetId":"1351620000000-987654",
               "SegmentDuration":"5",
               "Duration":"1003",
               "DurationMillis":"1003000",
               "Width":"1136",
               "Height":"640",
               "FrameRate":"30.00",
               "FileSize":"4718600",
               "Status":"Complete",
               "StatusDetail":""
            },
         ],
         "PipelineId":"1111111111111-abcde1",
         "Playlists":[
            {
               "Format":"HLSv3",
               "Name":"playlist-iPhone-lasagna.m3u8",
               "OutputKeys":[
                  "iphone/lasagna-1024k",
                  "iphone/lasagna-512k"
               ]
            }
         ],
         "Timing":{
               "SubmitTime":"1427212800000",
               "StartTime":"1427212856000",
               "FinishTime":"1427212875000"
         },
         "Status":"Complete"
      },
      {
         "Id":"4444444444444-abcde4",
         "Input":{
            "Key":"cooking/spaghetti.mp4",
            "FrameRate":"auto",
            "Resolution":"auto",
            "AspectRatio":"auto",
            "Interlaced":"auto",
            "Container":"mp4",
            "DetectedProperties":{
               "Width":"1280",
               "Height":"720",
               "FrameRate":"30.00",
               "FileSize":"5872000",
               "DurationMillis":"1003000"
            }
         },
         "Outputs":[
            {
               "Id":"3",
               "Key":"iphone/spaghetti-512k",
               "ThumbnailPattern":"iphone/th512k/spaghetti-{count}",
               "Rotate":"0",
               "PresetId":"1351620000000-456789",
               "SegmentDuration":"5",
               "Watermarks":[
                  {
                     "InputKey":"logo/128x64.png",
                     "PresetWatermarkId":"company logo 128x64"
                  }
               ],
               "Duration":"1003",
               "DurationMillis":"1003000",
               "Width":"1136",
               "Height":"640",
               "FrameRate":"30.00",
               "FileSize":"5872000",
               "Status":"Complete",
               "StatusDetail":""
            }
         ],
         "Playlists":[
            {
               "Format":"HLSv3",
               "Name":"playlist-iPhone-spaghetti.m3u8",
               "OutputKeys":[
                  "iphone/spaghetti-512k"
               ]
            }
         ],
         "UserMetadata":
            {
               "Food type":"Italian",
               "Cook book":"recipe notebook"
            },
         "Status":"Complete",
         "Timing":{
            "SubmitTime":"1427212800000",
            "StartTime":"1427212856000",
            "FinishTime":"1427212875000"
         }
      }
   ],
   "NextPageToken":null
}
```