# List Presets<a name="list-presets"></a>


+ [Description](#list-presets-description)
+ [Requests](#list-presets-requests)
+ [Responses](#list-presets-responses)
+ [Errors](#list-presets-response-errors)
+ [Examples](#list-presets-examples)

## Description<a name="list-presets-description"></a>

To get a list of all presets associated with the current AWS account, send a GET request to the `/2012-09-25/presets` resource\.

## Requests<a name="list-presets-requests"></a>

### Syntax<a name="list-presets-request-syntax"></a>

```
GET /2012-09-25/presets/[Ascending](#list-presets-request-ascending)=true|false&
                [PageToken](#list-presets-request-pageToken)=value for accessing the next page of 
                results HTTP/1.1 Content-Type: charset=UTF-8
Accept: */*
Host: elastictranscoder.Elastic Transcoder endpoint.amazonaws.com:443
x-amz-date: 20130114T174952Z
Authorization: AWS4-HMAC-SHA256
               Credential=AccessKeyID/request-date/Elastic Transcoder endpoint/elastictranscoder/aws4_request,
               SignedHeaders=host;x-amz-date;x-amz-target,
               Signature=calculated-signature
```

### Request Parameters<a name="list-presets-request-parameters"></a>

This operation takes the following request parameters\. Elastic Transcoder returns all of the presets available\.

**Ascending**  
To list presets in chronological order by the date and time that they were submitted, enter `true`\. To list presets in reverse chronological order, enter `false`\.

**PageToken**  
When Elastic Transcoder returns more than one page of results, use `PageToken` in subsequent `GET` requests to get each successive page of results\.

### Request Headers<a name="list-presets-request-headers"></a>

This operation uses only request headers that are common to all operations\. For information about common request headers, see [HTTP Header Contents](making-http-requests.md#http-request-header)\.

### Request Body<a name="list-presets-request-body"></a>

The JSON string in the request body contains the following objects\. 

## Responses<a name="list-presets-responses"></a>

### Syntax<a name="list-presets-response-syntax"></a>

```
Status: 200 OK
x-amzn-RequestId: c321ec43-378e-11e2-8e4c-4d5b971203e9
Content-Type: application/json
Content-Length: number of characters in the response
Date: Mon, 14 Jan 2013 06:01:47 GMT

{
   "Presets":[
      {
         "[Id](#list-presets-response-id)":"preset ID",
         "[Type](#list-presets-response-type)":"Custom|System",
         "[Name](#list-presets-response-name)":"preset name",
         "[Description](#list-presets-response-description)":"preset description",
         "[Container](#list-presets-response-container)":"flac|flv|fmp4|gif|mp3|mp4|mpg|mxf|oga|ogg|ts|wav|webm",
         "Audio":{
            "[Codec](#list-presets-response-audio-codec)":"AAC|flac|mp2|mp3|pcm|vorbis",
            "CodecOptions":{
               "[Profile](#list-preset-request-audio-codec-profile)":"auto|AAC-LC|HE-AAC|HE-AACv2",
               "[BitDepth](#list-preset-request-audio-codec-bit-depth)":"8|16|24|32",
               "[Signed](#list-preset-request-audio-codec-signed)":"Signed|Unsigned",
               "[BitOrder](#list-preset-request-audio-codec-bit-order)":"LittleEndian"
            },
            "[SampleRate](#list-presets-response-audio-sample-rate)":"auto|22050|32000|44100|48000|96000",
            "[BitRate](#list-presets-response-audio-bit-rate)":"audio bit rate of output file in kilobits/second",
            "[Channels](#list-presets-response-audio-channels)":"auto|0|1|2",
            "[AudioPackingMode](#list-preset-request-audio-packing-mode)":"SingleTrack|OneChannelPerTrack|
               OneChannelPerTrackWithMosTo8Tracks"
         },
         "Video":{
            "[Codec](#list-presets-response-video-codec)":"gif|H.264|mpeg2|vp8|vp9",
            "CodecOptions":{
               "[Profile](#list-presets-response-video-profile)":"baseline|main|high|0|1|2|3",
               "[Level](#list-presets-response-video-level)":"1|1b|1.1|1.2|1.3|2|2.1|2.2|
                  3|3.1|3.2|4|4.1",
               "[MaxReferenceFrames](#list-presets-response-video-max-reference-frames)":"maximum number of reference frames",
               "[MaxBitRate](#list-presets-response-video-max-bit-rate)":"maximum bit rate",
               "[BufferSize](#list-presets-response-video-buffer-size)":"maximum buffer size",
               "[InterlacedMode](#list-preset-request-video-interlace)":"Progressive|TopFirst|BottomFirst|Auto",
               "[ColorSpaceConversion](#list-preset-request-video-color-space)":"None|Bt709ToBt601|Bt601ToBt709|Auto",
               "[ChromaSubsampling](#list-preset-request-video-chroma)":"yuv420p|yuv422p",
               "[LoopCount](#list-preset-request-video-loop)":"Infinite|[0,100]"
            },
            "[KeyframesMaxDist](#list-presets-response-video-key-frames-max-dist)":"maximum frames between key frames",
            "[FixedGOP](#list-presets-response-video-fixed-gop)":"true|false",
            "[BitRate](#list-presets-response-video-bit-rate)":"auto|video bit rate of output file in 
               kilobits/second",
            "[FrameRate](#list-presets-response-video-frame-rate)":"auto|10|15|23.97|24|25|29.97|30|50|60",
            "[MaxFrameRate](#list-presets-response-video-max-frame-rate)":"10|15|23.97|24|25|29.97|30|50|60",
            "[MaxWidth](#list-presets-response-video-max-width)":"auto|[128,4096]",
            "[MaxHeight](#list-presets-response-video-max-height)":"auto|[96,3072]",
            "[SizingPolicy](#list-presets-response-video-sizing-policy)":"Fit|Fill|Stretch|Keep|ShrinkToFit|ShrinkToFill",
            "[PaddingPolicy](#list-presets-response-video-padding-policy)":"Pad|NoPad",
            "[DisplayAspectRatio](#list-presets-response-video-display-aspect-ratio)":"auto|1:1|4:3|3:2|16:9",
            "[Resolution](#list-presets-response-video-resolution)":"width in pixelsxheight in pixels",
            "[AspectRatio](#list-presets-response-video-aspect-ratio)":"auto|1:1|4:3|3:2|16:9",
            "[Watermarks](#list-presets-response-video-watermarks)":[
               {
                  "[Id](#list-presets-response-video-watermarks-id)":"unique identifier up to 40 characters",
                  "[MaxWidth](#list-presets-response-video-watermarks-max-width)":"[16,Video:MaxWidth]px|[0,100]%",
                  "[MaxHeight](#list-presets-response-video-watermarks-max-height)":"[16,Video:MaxHeight]px|[0,100]%", 
                  "[SizingPolicy](#list-presets-response-video-watermarks-sizing-policy)":"Fit|Stretch|ShrinkToFit",
                  "[HorizontalAlign](#list-presets-response-video-watermarks-horizontal-align)":"Left|Right|Center",
                  "[HorizontalOffset](#list-presets-response-video-watermarks-horizontal-offset)":"[0,100]%|[0,Video:MaxWidth]px",
                  "[VerticalAlign](#list-presets-response-video-watermarks-vertical-align)":"Top|Bottom|Center",
                  "[VerticalOffset](#list-presets-response-video-watermarks-vertical-offset)":"[0,100]%|[0,Video:MaxHeight]px",
                  "[Opacity](#list-presets-response-video-watermarks-opacity)":"[0,100]",
                  "[Target](#list-presets-response-video-watermarks-target)":"Content|Frame"
               },
               {...}
            ]
         },
         "Thumbnails":{
            "[Format](#list-presets-response-thumbnails-format)":"jpg|png",
            "[Interval](#list-presets-response-thumbnails-interval)":"number of seconds between thumbnails",
            "[MaxWidth](#list-presets-response-thumbnails-max-width)":"auto|[32,4096]",
            "[MaxHeight](#list-presets-response-thumbnails-max-height)":"auto|[32,3072]",
            "[SizingPolicy](#list-presets-response-thumbnails-sizing-policy)":"Fit|Fill|Stretch|Keep|ShrinkToFit|ShrinkToFill",
            "[PaddingPolicy](#list-presets-response-thumbnails-padding-policy)":"Pad|NoPad",
            "[Resolution](#list-presets-response-thumbnails-resolution)":"width in pixelsxheight in pixels",
            "[AspectRatio](#list-presets-response-thumbnails-aspect-ratio)":"auto|1:1|4:3|3:2|16:9"
         },
      },
      {...},
   ],
   "[NextPageToken](#list-presets-response-next-page-token)":value for accessing the next page of results|null
}
```

### Response Headers<a name="list-presets-response-headers"></a>

This operation uses only response headers that are common to most responses\. For information about common response headers, see [HTTP Responses](making-http-requests.md#http-response-header)\.

### Response Body<a name="list-presets-response-body"></a>

The JSON string in the request body contains the following objects\. For more detail about the individual objects, see [Request Body](create-preset.md#create-preset-request-body) in the topic [Create Preset](create-preset.md)\.

**Id**  
Identifier for the new preset\. You use this value to get settings for the preset or to delete it\. 

**Type**  
Whether the preset is a default preset provided by Elastic Transcoder \(`System`\) or a preset that you have defined \(`Custom`\)\.

**Name**  
The name of the preset\. We recommend that the name be unique within the AWS account, but uniqueness is not enforced\.  
Constraints: Maximum 40 characters

**Description**  
A description of the preset\.  
Constraints: Maximum 255 characters

**Container**  
The container type for the output file\. Valid values are `flac`, `flv`, `fmp4`, `gif`, `mp3`, `mp4`, `mpg`, `mxf`, `oga`, `ogg`, `ts`, `wav`, and `webm`\. The following table shows the supported codecs for containers\.      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)

**Audio:Codec**  
The audio codec for the output file\. Valid values are `AAC`, `flac`, `mp2`, `mp3`, `pcm`, and `vorbis`\. The following table shows the available combinations of containers and audio codecs\.      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)

** \(AAC Only\) Audio:CodecOptions:Profile**  
If you specified `AAC` for `Audio:Codec`, choose the AAC profile for the output file\. Elastic Transcoder supports the following profiles:  

+ `auto`: If you specify `auto`, Elastic Transcoder selects the profile based on the bit rate selected for the output file\.

+ `AAC-LC`: The most common AAC profile\. Use for bit rates larger than 64 kbps\. For more information, see [ Advanced Audio Coding\.](http://en.wikipedia.org/wiki/Advanced_Audio_Coding)

+ `HE-AAC`: Not supported on some older players and devices\. Use for bit rates between 40 and 80 kbps\. For more information, see [ High\-Efficiency Advanced Audio Coding\.](http://en.wikipedia.org/wiki/HE-AAC)

+ `HE-AACv2`: Not supported on some players and devices\. Use for bit rates less than 48 kbps\. For more information, see [High\-Efficiency Advanced Audio Coding\.](http://en.wikipedia.org/wiki/HE-AAC)\.
All outputs in a `Smooth` playlist must have the same value for `Profile`\.  
If you created any presets before AAC profiles were added, Elastic Transcoder automatically updated your presets to use AAC\-LC\.
For more information about AAC, go to [Audio Profiles](http://en.wikipedia.org/wiki/MPEG-4_Part_3#Audio_Profiles) in the Wikipedia entry "MPEG\-4 Part 3\."

** \(Optional, FLAC/PCM Only\) Audio:CodecOptions:BitDepth**  
The bit depth of a sample is how many bits of information are included in the audio samples\. The higher the bit depth, the better the audio, but the larger the file\.  
Valid values for the `FLAC` codec are `16` and `24`\.  
Valid values for the `PCM` codec are `8`, `16`, `24`, and `32`\.

** \(Optional, PCM Only\) Audio:CodecOptions:Signed**  
Whether audio samples are represented with negative and positive numbers \(signed\) or only positive numbers \(unsigned\)\.  
Valid values are `Signed` and `Unsigned`\.  
The most common value is `Signed`\.

** \(Optional, PCM Only\) Audio:CodecOptions:BitOrder**  
The order the bits of a PCM sample are stored in\.  
 The supported value is `LittleEndian`\.

**Audio:SampleRate**  
The sample rate of the audio stream in the output file, in hertz\. Valid values are:  
`auto`, `22050`, `32000`, `44100`, `48000`, `96000`  
If you specify `auto`, Elastic Transcoder automatically detects the sample rate\.  
If you are using `mxf` for your output container, you must use a sample rate of `48000`\.

**Audio:BitRate**  
The bit rate of the audio stream in the output file, in kilobits/second\. Enter an integer between 64 and 320, inclusive\. 

**Audio:Channels**  
The number of audio channels in the output file\. The following values are valid:  
`auto`, `0`, `1`, `2`  
One channel carries the information played by a single speaker\. For example, a stereo track with two channels sends one channel to the left speaker, and the other channel to the right speaker\. The output channels are organized into tracks\. If you want Elastic Transcoder to automatically detect the number of audio channels in the input file and use that value for the output file, select `auto`\.      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)
For more information about how digital audio works, see [Digital Audio](audio.md)\. For more information about how Elastic Transcoder organizes channels and tracks, see `Audio:AudioPackingMode`\.

**\(MXF with PCM Only\) Audio:AudioPackingMode**  
The method of organizing audio channels and tracks\. Use `Audio:Channels` to specify the number of channels in your output, and `Audio:AudioPackingMode` to specify the number of tracks and their relation to the channels\. If you do not specify an `Audio:AudioPackingMode`, Elastic Transcoder uses `SingleTrack`\.  
The following values are valid:  
`SingleTrack`, `OneChannelPerTrack`, and `OneChannelPerTrackWithMosTo8Tracks`    
**Audio:AudioPackingMode:SingleTrack**  
Elastic Transcoder creates a single track for your output\. The track can have up to eight channels\. Use `SingleTrack` for all non\-`mxf` containers\.      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)  
**\(MXF Only\) Audio:AudioPackingMode:OneChannelPerTrack**  
Elastic Transcoder creates a new track for every channel in your output\. Your output can have up to eight single\-channel tracks\.      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)  
**\(MXF Only\) Audio:AudioPackingMode:OneChannelPerTrackWithMosTo8Tracks**  
Elastic Transcoder creates eight single\-channel tracks for your output\. All tracks that do not contain audio data from an input channel are MOS, or Mit Out Sound, tracks\.      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)
For more information on channels and tracks, see [Digital Audio](audio.md)\.

**Video:Codec**  
The video codec for the output file\. Valid values are  `gif`, `H.264`, `mpeg2`, `vp8`, and `vp9`\. The following table shows the available combinations of containers and video codecs\.      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)
For more information about the H\.264 video\-compression format, go to the Wikipedia page on [H\.264/MPEG\-4 AVC](http://en.wikipedia.org/wiki/H.264/MPEG-4_AVC)\.  
For more information about VP8, go to [VP8](https://en.wikipedia.org/wiki/VP8)\. For more information about VP9, go to [VP9](https://en.wikipedia.org/wiki/VP9)\.

**\(H\.264/VP8 Only\) Video:CodecOptions:Profile**  
If you specified `H.264` for `Video:Codec`, the H\.264 profile that you want to use for the output file\. Elastic Transcoder supports the following profiles:  

+ `baseline`: The profile most commonly used for video conferencing and for mobile applications\.

+ `main`: The profile used for standard\-definition digital TV broadcasts\.

+ `high`: The profile used for high\-definition digital TV broadcasts and for Blu\-ray discs\.
If you specified `vp8` for the video codec, the vp8 profile that you want to use for the output file\. Elastic Transcoder supports the following profiles: `0`, `1`, `2`, `3`\. You can specify `0`, `1`, `2`, or `3` only when the container type is `webm`\.  
For more information about profiles, see [Profiles](http://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Profiles) in the Wikipedia entry "H\.264/MPEG\-4 AVC\."

**\(H\.264 Only\) Video:CodecOptions:Level**  
Applicable only when the value of `Video:Codec` is `H.264`\. The H\.264 level that you want to use for the output file\. Elastic Transcoder supports the following levels:  
`1`, `1b`, `1.1`, `1.2`, `1.3`, `2`, `2.1`, `2.2`, `3`, `3.1`, `3.2`, `4`, `4.1`  
For more information about levels, see [Levels](http://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Levels) in the Wikipedia entry "H\.264/MPEG\-4 AVC\."

**\(H\.264 Only\) Video:CodecOptions:MaxReferenceFrames **  
Applicable only when the value of `Video:Codec` is `H.264`\. The maximum number of previously decoded frames to use as a reference for decoding future frames\. Valid values are integers 0 through 16, but we recommend that you not use a value greater than:  
`Min(Floor(Maximum decoded picture buffer in macroblocks * 256 / (Width in pixels * Height in pixels)), 16)`  
where:  

+ `Width in pixels` and `Height in pixels` represent either `Video:MaxWidth` and `Video:MaxHeight`, or `Video:Resolution`\.

+ `Maximum decoded picture buffer in macroblocks` depends on the value of the `Video:CodecOptions:Level` object\. \(A macroblock is a block of pixels measuring 16x16\.\) See the table below\.
For more information about encoding based on previously encoded pictures, see [Decoded picture buffering](http://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Decoded_picture_buffering) in the Wikipedia entry "H\.264/MPEG\-4 AVC\." Note that the Wikipedia calculation for maximum decoded picture buffer, which is similar to the calculation for maximum reference frames, uses macroblocks instead of pixels for the width and height of the video\.      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)

** \(Optional, H\.264/MPEG2/VP8/VP9 only\) Video:CodecOptions:MaxBitRate**  
The maximum number of kilobits per second in the output video\. Specify a value between 16 and 62,500, inclusive\.   
If you specify `auto` for `BitRate`, Elastic Transcoder uses the bit rate of the input video as the average bit rate of the output video\. `MaxBitRate` allows you to cap the bit rate of the output video, which is useful when the maximum bit rate supported by a target device is lower than the bit rate of the input video\. Reducing the maximum bit rate might reduce the quality of the video\.

** \(Optional, H\.264/MPEG2/VP8/VP9 only\) Video:CodecOptions:BufferSize**  
The maximum number of kilobits in any *x* seconds of the output video\. This window is commonly 10 seconds, the standard segment duration when you're using ts for the container type of the output video\. Specify an integer greater than 0\. If you specify `MaxBitRate` and omit `BufferSize`, Elastic Transcoder sets `BufferSize` to 10 times the value of `MaxBitRate`\.

** \(Optional, H\.264/MPEG2 Only\) Video:CodecOptions:InterlacedMode**  
The interlace mode for the output video\.  
Interlaced video is used to double the perceived frame rate for a video by interlacing two fields \(one field on every other line, the other field on the other lines\) so that the human eye registers multiple pictures per frame\. Interlacing reduces the bandwidth required for transmitting a video, but can result in blurred images and flickering\.  
The two sets of lines are known as fields, and an interlaced frame splits two images across the fields:  

![\[Interlace Fields.\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/)
Valid values are `Progressive` \(no interlacing, top to bottom\), `TopFirst` \(top field first\), `BottomFirst` \(bottom field first\), and `Auto`\.  
If `InterlaceMode` is not specified, Elastic Transcoder uses `Progressive` for the output\. If `Auto` is specified, Elastic Transcoder interlaces the output\.  
For more information, go to the Wikipedia page [Interlaced video](http://en.wikipedia.org/wiki/Interlaced_video)\.

** \(Optional, H\.264/MPEG2 Only\) Video:CodecOptions:ColorSpaceConversion**  
The color space conversion Elastic Transcoder applies to the output video\. Color spaces are the algorithms used by the computer to store information about how to render color\. `Bt.601` is the standard for standard definition video, while `Bt.709` is the standard for high definition video\.  
Valid values are `None`, `Bt709toBt601`, `Bt601toBt709`, and `Auto`\.  
If you chose `Auto` for `ColorSpaceConversionMode` and your output is interlaced, your frame rate is one of `23.97`, `24`, `25`, `29.97`, `50`, or `60`, your `SegmentDuration` is null, and you are using one of the resolution changes from the graph below, Elastic Transcoder applies the following color space conversions:      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)
Elastic Transcoder may change the behavior of the `ColorspaceConversionMode` `Auto` mode in the future\. All outputs in a playlist must use the same `ColorSpaceConversionMode`\.
If you do not specify a `ColorSpaceConversionMode`, Elastic Transcoder does not change the color space of a file\.  
If you are unsure what `ColorSpaceConversionMode` was applied to your output file, you can check the `AppliedColorSpaceConversion` parameter included in your job response\. If your job does not have an `AppliedColorSpaceConversion` in its response, no `ColorSpaceConversionMode` was applied\.  
For more information about color space, go to the Wikipedia page [Color space](http://en.wikipedia.org/wiki/Color_space)\. For more information about `Bt.601` and `Bt.709`, go to the Wikipedia pages [Rec\. 601](http://en.wikipedia.org/wiki/Rec._601) and [Rec\. 709](http://en.wikipedia.org/wiki/Rec._709)\.

** Video:CodecOptions:ChromaSubsampling**  
The sampling pattern for the chroma \(color\) channels of the output video\. Valid values are `yuv420p` and `yuv422p`\.  
`yuv420p` samples the chroma information of every other horizontal and every other vertical line, `yuv422p` samples the color information of every horizontal line and every other vertical line\.  
To learn more about chroma subsampling, go to the Wikipedia page [Chroma subsampling](http://en.wikipedia.org/wiki/Chroma_subsampling)\.

 **\(Gif Only\) Video:CodecOptions:LoopCount**  
The number of times you want the output gif to loop\.  
Valid values are `Infinite` and integers between `0` and `100`, inclusive\.

** \(H\.264/MPEG2/VP8 Only\) Video:KeyframesMaxDist**  
The maximum number of frames between key frames\. Not applicable for containers of type `gif`\. Key frames are fully encoded frames; the frames between key frames are encoded based, in part, on the content of the key frames\. The value is an integer formatted as a string; valid values are between 1 \(every frame is a key frame\) and 100000, inclusive\. A higher value results in higher compression but might also discernibly decrease video quality\.   
For `Smooth` outputs, the `FrameRate` must have a constant ratio to the `KeyframesMaxDist`\. This allows `Smooth` playlists to switch between different quality levels while the file is being played\.  
For example, an input file can have a `FrameRate` of 30 with a `KeyframesMaxDist` of 90\. The output file then needs to have a ratio of 1:3\. Valid outputs would have `FrameRate` of 30, 25, and 10, and `KeyframesMaxDist` of 90, 75, and 30, respectively\.  
Alternately, this can be achieved by setting `FrameRate` to auto and having the same values for `MaxFrameRate` and `KeyframesMaxDist`\.  
For more information about key frames, see the Wikipedia entry [Video compression picture types](http://en.wikipedia.org/wiki/Video_compression_picture_types)\.

** \(H\.264/MPEG2/VP8 Only\) Video:FixedGOP**  
Whether to use a fixed value for `Video:FixedGOP`\. Not applicable for containers of type `gif`\. Valid values are `true` and `false`:  

+ `true`: Elastic Transcoder uses the value of `Video:KeyframesMaxDist` for the distance between key frames \(the number of frames in a group of pictures, or GOP\)\.

+ `false`: The distance between key frames can vary\.
`FixedGOP` must be set to `true` for `fmp4` containers\.

**Video:BitRate**  
The bit rate of the video stream in the output file, in kilobits/second\. You can configure variable bit rate or constant bit rate encoding:  

+ **Variable bit rate encoding:** Specify **auto**\. Elastic Transcoder optimizes the bit rate and maintains a consistent quality for each frame of the output\.

+ **Constant bit rate encoding:** Specify the bit rate\.
**If you specified `H.264` for `Video:Codec`:** Valid values depend on the values of the `Video:CodecOptions:Level` and `Video:CodecOptions:Profile` objects\.   
If you specified `vp8` for `Video:Codec`, do not use the following table; `Level` applies only when the video codec is H\.264\.
If you specify a value other than `auto`, we recommend that you specify a value less than or equal to the maximum H\.264\-compliant value listed in the following table for your level and profile:      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)

**Video:FrameRate**  
The frames per second for the video stream in the output file\. The following values are valid:  
`auto`, `10`, `15`, `23.97`, `24`, `25`, `29.97`, `30`, `50`, `60`  
If you want to preserve the frame rate of the input file and use it for the output file, specify `auto`\.  
**If you specified `H.264` for Video:Codec:** If you specify a frame rate, we recommend that you perform the following calculation:   
`Frame rate = maximum recommended decoding speed in luma samples/second / (width in pixels * height in pixels)`  
where:  

+ `width in pixels` and `height in pixels` represent the `Video:Resolution` of the output video\.

+ `maximum recommended decoding speed in Luma samples/second` is less than or equal to the maximum value listed in the following table, based on the value that you specified for `Video:CodecOptions:Level`\.
If you specified `vp8` for `Video:Codec`, do not use the previous equation or the following table; `Level` applies only when the video codec is H\.264\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)

**Video:MaxFrameRate**  
If you specify `auto` for `FrameRate`, Elastic Transcoder uses the frame rate of the input video for the frame rate of the output video, up to the maximum frame rate\. If you do not specify a `MaxFrameRate`, Elastic Transcoder will use a default of `30`\.  
Specify the maximum frame rate that you want Elastic Transcoder to use when the frame rate of the input video is greater than either the desired maximum frame rate of the output video or the default maximum frame rate\. The following values are valid:  
`10`, `15`, `23.97`, `24`, `25`, `29.97`, `30`, `50`, `60`  
Elastic Transcoder uses the highest supported frame rate that meets both of the following criteria:  

+ The frame rate is less than or equal to the maximum frame rate\.

+ The frame rate divides into the input frame rate evenly, with no remainder\.
For example, if you have an input file with a frame rate of 50 and specify a value of 30 for `MaxFrameRate`, Elastic Transcoder produces an output video for which the frame rate is 25 frames per second, because 25 is less than 30, and 50 divided by 25 is 2\.

**Video:MaxWidth**  
The maximum width of the output video in pixels\. If you specify `auto`, Elastic Transcoder uses 1920 \(Full HD\) as the default value\. If you specify a numeric value, enter an even integer between 128 and 4096, inclusive\.  
For more information, see `Video:MaxHeight`\.

**Video:MaxHeight**  
The maximum height of the output video in pixels\. If you specify `auto`, Elastic Transcoder uses 1080 \(Full HD\) as the default value\. If you specify a numeric value, enter an even integer between 96 and 3072, inclusive\.  
**If you specified `H.264` for `Video:Codec`:** We recommend that you specify values for `MaxWidth` and `MaxHeight` so the product of the two values is less than or equal to the applicable value in the following table\.  
If you specified `vp8` for `Video:Codec`, do not use the following table; `Level` applies only when the video codec is H\.264\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)

**Video:SizingPolicy**  
A value that controls scaling of the output video:  

+ **Fit:** Elastic Transcoder scales the output video so it matches the value that you specified in either `MaxWidth` or `MaxHeight` without exceeding the other value\.

+ **Fill:** Elastic Transcoder scales the output video so it matches the value that you specified in either `MaxWidth` or `MaxHeight` and matches or exceeds the other value\. Elastic Transcoder centers the output video and then crops it to the dimension \(if any\) that exceeds the maximum value\. 

+ **Stretch:** Elastic Transcoder stretches the output video to match the values that you specified for `MaxWidth` and `MaxHeight`\. If the relative proportions of the input video and the output video are different, the output video will be distorted\.

+ **Keep:** Elastic Transcoder does not scale the output video\. If either dimension of the input video exceeds the values that you specified for `MaxWidth` and `MaxHeight`, Elastic Transcoder crops the output video\.

+ **ShrinkToFit:** Elastic Transcoder scales the output video down so that its dimensions match the values that you specified for at least one of `MaxWidth` and `MaxHeight` without exceeding either value\. If you specify this option, Elastic Transcoder does not scale the video up\.

+ **ShrinkToFill:** Elastic Transcoder scales the output video down so that its dimensions match the values that you specified for at least one of `MaxWidth` and `MaxHeight` without dropping below either value\. If you specify this option, Elastic Transcoder does not scale the video up\.
The following table shows possible effects of `SizingPolicy` settings on the output video:      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)

**Video:PaddingPolicy**  
When you set `PaddingPolicy` to `Pad`, Elastic Transcoder might add black bars to the top and bottom and/or left and right sides of the output video to make the total size of the output video match the values that you specified for `MaxWidth` and `MaxHeight`\. For more information, see the table at `Video:SizingPolicy`\.

**Video:DisplayAspectRatio**  
The value that Elastic Transcoder adds to the metadata in the output file\. If you set `DisplayAspectRatio` to `auto`, Elastic Transcoder chooses an aspect ratio that ensures square pixels\. If you specify another option, Elastic Transcoder sets that value in the output file\. 

**Video:Resolution**  
To better control resolution and aspect ratio of output videos, we recommend that you use the Video—Option 1 settings, `MaxWidth`, `MaxHeight`, `SizingPolicy`, `PaddingPolicy`, and `DisplayAspectRatio` instead of the two Video—Option 2 settings, `Resolution` and `AspectRatio`\. The two groups of settings are mutually exclusive\. Do not use them together\.
The width and height of the video in the output file, in pixels\. Valid values are `auto` and *width*x*height*:  

+ `auto`: Elastic Transcoder attempts to preserve the width and height of the input file, subject to the following rules\.

+ `widthxheight`: The width and height of the output video in pixels\. 
Note the following about specifying the width and height:  

+ The width must be an even integer between 128 and 4096, inclusive\. 

+ The height must be an even integer between 96 and 3072, inclusive\. 

+ If you specify a resolution that is less than the resolution of the input file, Elastic Transcoder rescales the output file to the lower resolution\. 

+ If you specify a resolution that is greater than the resolution of the input file, Elastic Transcoder rescales the output to the higher resolution\.

+ We recommend that you specify a resolution for which the product of width and height is less than or equal to the applicable value in the following table:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)

**Video:AspectRatio**  
To better control resolution and aspect ratio of output videos, we recommend that you use the values `MaxWidth`, `MaxHeight`, `SizingPolicy`, `PaddingPolicy`, and `DisplayAspectRatio` instead of `Resolution` and `AspectRatio`\.
The display aspect ratio of the video in the output file\. The following values are valid:  
`auto`, `1:1`, `4:3`, `3:2`, `16:9`  
If you specify `auto`, Elastic Transcoder tries to preserve the aspect ratio of the input file\.  
If you specify an aspect ratio for the output file that differs from aspect ratio of the input file, Elastic Transcoder adds pillarboxing \(black bars on the sides\) or letterboxing \(black bars on the top and bottom\) to maintain the aspect ratio of the active region of the video\.

**Video:Watermarks**  
Settings for the size, position, scale, and opacity of graphics that you want Elastic Transcoder to overlay over videos that are transcoded using this preset\. You can specify settings for up to four watermarks\. Watermarks appear for the duration of the transcoded video\.   
Watermarks can be in `.png` or `.jpg` format\. If you want to display a watermark that is not rectangular, use the `.png` format, which supports transparency\.  
When you create a job that uses this preset, you specify the `.png` or `.jpg` graphics that you want Elastic Transcoder to include in the transcoded videos\. Elastic Transcoder does not require you to specify as many watermarks in each job output as you specified in the corresponding preset\. For example, you might specify settings for four watermarks in a preset and specify only one watermark in a job output\.   
To configure watermark settings so your graphic is not distorted, set the value of `SizingPolicy` to `ShrinkToFit`, and set the values of `MaxWidth` and `MaxHeight` to the same percentage\. If you want the graphic to appear in the same size as the original, set `MaxWidth` and `MaxHeight` to 100%\.  
For more information, see [Watermarks](watermarks.md)\.

**Video:Watermarks:Id**  
A unique identifier for the settings for one watermark\. The value of `Id` can be up to 40 characters long\. You can specify settings for up to four watermarks\. 

**Video:Watermarks:MaxWidth**  
The maximum width of the watermark in one of the following formats:  

+ *number of pixels*`px`: The minimum value is 16 pixels, and the maximum value is the value of `Video:MaxWidth`\. 

+ *integer percentage*`%`: The range of valid values is 0 to 100\. Use the value of `Target` to specify whether you want Elastic Transcoder to include the black bars that are added by Elastic Transcoder, if any, in the calculation\.

**Video:Watermarks:MaxHeight**  
The maximum height of the watermark in one of the following formats:  

+ *number of pixels*`px`: The minimum value is 16 pixels, and the maximum value is the value of `Video:MaxHeight`\. 

+ *integer percentage*`%`: The range of valid values is 0 to 100\. Use the value of `Target` to specify whether you want Elastic Transcoder to include the black bars that are added by Elastic Transcoder, if any, in the calculation\.

**Video:Watermarks:SizingPolicy**  
A value that controls scaling of the watermark:  

+ **Fit:** Elastic Transcoder scales the watermark so it matches the value that you specified in either `MaxWidth` or `MaxHeight` without exceeding the other value\.

+ **Stretch:** Elastic Transcoder stretches the watermark to match the values that you specified for `MaxWidth` and `MaxHeight`\. If the relative proportions of the watermark and the values of `MaxWidth` and `MaxHeight` are different, the watermark will be distorted\.

+ **ShrinkToFit:** Elastic Transcoder scales the watermark down so that its dimensions match the values that you specified for at least one of `MaxWidth` and `MaxHeight` without exceeding either value\. If you specify this option, Elastic Transcoder does not scale the watermark up\.

**Video:Watermarks:HorizontalAlign**  
The horizontal position of the watermark unless you specify a nonzero value for `HorizontalOffset`:  

+ **Left:** The left edge of the watermark is aligned with the left border of the video\.

+ **Right:** The right edge of the watermark is aligned with the right border of the video\.

+ **Center:** The watermark is centered between the left and right borders\.

**Video:Watermarks:HorizontalOffset**  
The amount by which you want the horizontal position of the watermark to be offset from the position specified by `HorizontalAlign`:   

+ *number of pixels*`px`: The minimum value is 0 pixels, and the maximum value is the value of `Video:MaxWidth`\. 

+ *integer percentage*`%`: The range of valid values is 0 to 100\.
For example, if you specify `Left` for `HorizontalAlign` and `5px` for `HorizontalOffset`, the left side of the watermark appears 5 pixels from the left border of the output video\.  
`HorizontalOffset` is valid only when the value of `HorizontalAlign` is `Left` or `Right`\.  
If you specify an offset that causes the watermark to extend beyond the left or right border and Elastic Transcoder has not added black bars, the watermark is cropped\. If Elastic Transcoder has added black bars, the watermark extends into the black bars\. If the watermark extends beyond the black bars, it is cropped\.  
Use the value of `Target` to specify whether you want Elastic Transcoder to include the black bars that are added by Elastic Transcoder, if any, in the offset calculation\.

**Video:Watermarks:VerticalAlign**  
The vertical position of the watermark unless you specify a nonzero value for `VerticalOffset`:  

+ **Top:** The top edge of the watermark is aligned with the top border of the video\.

+ **Bottom:** The bottom edge of the watermark is aligned with the bottom border of the video\.

+ **Center:** The watermark is centered between the top and bottom borders\.

**Video:Watermarks:VerticalOffset**  
The amount by which you want the vertical position of the watermark to be offset from the position specified by `VerticalAlign`:   

+ *number of pixels*`px`: The minimum value is 0 pixels, and the maximum value is the value of `Video:MaxHeight`\. 

+ *integer percentage*`%`: The range of valid values is 0 to 100\.
For example, if you specify `Top` for `VerticalAlign` and `5px` for `VerticalOffset`, the top of the watermark appears 5 pixels from the top border of the output video\.  
`VerticalOffset` is valid only when the value of `VerticalAlign` is `Top` or `Bottom`\.  
If you specify an offset that causes the watermark to extend beyond the top or bottom border and Elastic Transcoder has not added black bars, the watermark is cropped\. If Elastic Transcoder has added black bars, the watermark extends into the black bars\. If the watermark extends beyond the black bars, it is cropped\.  
Use the value of `Target` to specify whether you want Elastic Transcoder to include the black bars that are added by Elastic Transcoder, if any, in the offset calculation\.

**Video:Watermarks:Opacity**  
A percentage that indicates how much you want a watermark to obscure the video in the location where it appears\. Valid values are 0 \(the watermark is invisible\) to 100 \(the watermark completely obscures the video in the specified location\)\. The data type of `Opacity` is `float`\.  
Elastic Transcoder supports transparent `.png` graphics\. If you use a transparent `.png`, the transparent portion of the video appears as if you had specified a value of 0 for `Opacity`\. The `.jpg` file format doesn't support transparency\.

**Video:Watermarks:Target**  
A value that determines how Elastic Transcoder interprets values that you specified for `Video:Watermarks:HorizontalOffset`, `Video:Watermarks:VerticalOffset`, `Video:Watermarks:MaxWidth`, and `Video:Watermarks:MaxHeight`:   

+ **Content:** `HorizontalOffset` and `VerticalOffset` values are calculated based on the borders of the video **excluding** black bars added by Elastic Transcoder, if any\.

  In addition, `MaxWidth` and `MaxHeight`, if specified as a percentage, are calculated based on the borders of the video **excluding** black bars added by Elastic Transcoder, if any\.

+ **Frame:** `HorizontalOffset` and `VerticalOffset` values are calculated based on the borders of the video **including** black bars added by Elastic Transcoder, if any\.

  In addition, `MaxWidth` and `MaxHeight`, if specified as a percentage, are calculated based on the borders of the video **including** black bars added by Elastic Transcoder, if any\.

**\(Video Only\) Thumbnails:Format**  
The format of thumbnails, if any\. Valid formats are `jpg` and `png`\.   
You specify whether you want Elastic Transcoder to create thumbnails when you create a job\. For more information, see [ThumbnailPattern](create-job.md#create-job-request-output-thumbnail-pattern)\.

**\(Video Only\) Thumbnails:Interval**  
The approximate number of seconds between thumbnails\. The value must be an integer\. The actual interval can vary by several seconds from one thumbnail to the next\.

**\(Video Only\) Thumbnails:MaxWidth**  
The maximum width of thumbnails, in pixels\. If you specify `auto`, Elastic Transcoder uses 1920 \(Full HD\) as the default value\. If you specify a numeric value, enter an even integer between 32 and 4096, inclusive\.

**\(Video Only\) Thumbnails:MaxHeight**  
The maximum height of thumbnails, in pixels\. If you specify `auto`, Elastic Transcoder uses 1080 \(Full HD\) as the default value\. If you specify a numeric value, enter an even integer between 32 and 3072, inclusive\.

**\(Video Only\) Thumbnails:SizingPolicy**  
A value that controls scaling of thumbnails:  

+ **Fit:** Elastic Transcoder scales thumbnails so they match the value that you specified in thumbnail `MaxWidth` or `MaxHeight` settings without exceeding the other value\.

+ **Fill:** Elastic Transcoder scales thumbnails so they match the value that you specified in thumbnail `MaxWidth` or `MaxHeight` settings and matches or exceeds the other value\. Elastic Transcoder centers the image in thumbnails and then crops to the dimension, if any, that exceeds the maximum value\. 

+ **Stretch:** Elastic Transcoder stretches thumbnails to match the values that you specified for thumbnail `MaxWidth` and `MaxHeight` settings\. If the relative proportions of the input video and thumbnails are different, the thumbnails will be distorted\.

+ **Keep:** Elastic Transcoder does not scale thumbnails\. If either dimension of the input video exceeds the values that you specified for thumbnail `MaxWidth` and `MaxHeight` settings, Elastic Transcoder crops the thumbnails\.

+ **ShrinkToFit:** Elastic Transcoder scales thumbnails down so that their dimensions match the values that you specified for at least one of thumbnail `MaxWidth` and `MaxHeight` without exceeding either value\. If you specify this option, Elastic Transcoder does not scale thumbnails up\.

+ **ShrinkToFill:** Elastic Transcoder scales thumbnails down so that their dimensions match the values that you specified for at least one of `MaxWidth` and `MaxHeight` without dropping below either value\. If you specify this option, Elastic Transcoder does not scale thumbnails up\.
The following table shows possible effects of `SizingPolicy` settings on thumbnails:      
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/elastictranscoder/latest/developerguide/list-presets.html)

**\(Video Only\) Thumbnails:PaddingPolicy**  
When you set `PaddingPolicy` to `Pad`, Elastic Transcoder might add black bars to the top and bottom and/or left and right sides of thumbnails to make the total size of the thumbnails match the values that you specified for thumbnail `MaxWidth` and `MaxHeight` settings\. For more information, see the table at `Thumbnails:SizingPolicy`\.

**\(Video Only\) Thumbnails:Resolution**  
To better control resolution and aspect ratio of thumbnails, we recommend that you use the thumbnail values `MaxWidth`, `MaxHeight`, `SizingPolicy`, and `PaddingPolicy` instead of `Resolution` and `AspectRatio`\. The two groups of settings are mutually exclusive\. Do not use them together\.
The width and height of thumbnail files in pixels, in the format `Width`x`Height`, where both values are even integers\. The values cannot exceed the width and height that you specified in the `Video:Resolution` object\.

**\(Video Only\) Thumbnails:AspectRatio**  
To better control resolution and aspect ratio of thumbnails, we recommend that you use the thumbnail values `MaxWidth`, `MaxHeight`, `SizingPolicy`, and `PaddingPolicy` instead of `Resolution` and `AspectRatio`\.
The aspect ratio of thumbnails\. The following values are valid:  
`auto`, `1:1`, `4:3`, `3:2`, `16:9`  
If you specify `auto`, Elastic Transcoder tries to preserve the aspect ratio of the video in the output file\.

**NextPageToken**  
A value that you use to access the second and subsequent pages of results, if any\. When the presets fit on one page or when you've reached the last page of results, the value of `NextPageToken` is `null`\.

## Errors<a name="list-presets-response-errors"></a>

For information about Elastic Transcoder exceptions and error messages, see [Handling Errors in Elastic Transcoder](error-handling.md)\.

## Examples<a name="list-presets-examples"></a>

The following example request creates a preset named `DefaultPreset`\.

### Sample Request<a name="list-presets-examples-sample-request"></a>

```
GET /2012-09-25/presets HTTP/1.1
Content-Type: charset=UTF-8
Accept: */*
Host: elastictranscoder.Elastic Transcoder endpoint.amazonaws.com:443
x-amz-date: 20130114T174952Z
Authorization: AWS4-HMAC-SHA256
               Credential=AccessKeyID/request-date/Elastic Transcoder endpoint/elastictranscoder/aws4_request,
               SignedHeaders=host;x-amz-date;x-amz-target,
               Signature=calculated-signature
```

### Sample Response<a name="list-presets-examples-sample-response"></a>

```
Status: 200 OK
x-amzn-RequestId: c321ec43-378e-11e2-8e4c-4d5b971203e9
Content-Type: application/json
Content-Length: number of characters in the response
Date: Mon, 14 Jan 2013 06:01:47 GMT

{
   "Presets":[
      {
         "Id":"5555555555555-abcde5",
         "Type":"Custom",
         "Name":"DefaultPreset",
         "Description":"Use for published videos",
         "Container":"mp4",
         "Audio":{
            "BitRate":"96",
            "Channels":"2",
            "Codec":"AAC",
            "CodecOptions":{
               "Profile":"AAC-LC"
            },
            "SampleRate":"44100"
         },
         "Video":{
            "Codec":"H.264",
            "CodecOptions":{
               "Profile":"main",
               "Level":"2.2",
               "MaxReferenceFrames":"3",
               "MaxBitRate":"",
               "BufferSize":"",
               "InterlacedMode":"Progressive",
               "ColorSpaceConversionMode":"None"
            },
            "KeyframesMaxDist":"240",
            "FixedGOP":"false",
            "BitRate":"1600",
            "FrameRate":"auto",
            "MaxFrameRate":"30",
            "MaxWidth":"auto",
            "MaxHeight":"auto",
            "SizingPolicy":"Fit",
            "PaddingPolicy":"Pad",
            "DisplayAspectRatio":"auto",
            "Watermarks":[
               {
                  "Id":"company logo",
                  "MaxWidth":"20%",
                  "MaxHeight":"20%", 
                  "SizingPolicy":"ShrinkToFit",
                  "HorizontalAlign":"Right",
                  "HorizontalOffset":"10px",
                  "VerticalAlign":"Bottom",
                  "VerticalOffset":"10px",
                  "Opacity":"55.5",
                  "Target":"Content"
               }
            ]
         }
         "Thumbnails":{
            "Format":"png",
            "Interval":"120",
            "MaxWidth":"auto",
            "MaxHeight":"auto",
            "SizingPolicy":"Fit",
            "PaddingPolicy":"Pad"
         },
      },
      {...}
   ]
}
```