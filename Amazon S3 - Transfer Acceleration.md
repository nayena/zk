# Amazon S3 - Transfer Acceleration

When transferring data to S3 from your client with transfer acceleration enabled at the bucket level, the request will go via one of the CloudFront Edge Locations, from here the transfer request will then be routed through a high speed optimized AWS network path to Amazon S3.

When using transfer acceleration you should **be aware that there is a cost**. Whereas normal data transfer into amazon S3 is free from the internet, with transfer acceleration, this is a cost associated per GB depending on which edge location is used. 

Also, there is an increased cost for any data transferred **out** of S3, either to the internet or to another Region, again due to the edge location acceleration involved.

As a result, to enable transfer acceleration your bucket name **must** be DNS compliant and *not contain any periods at all*. Also, to make use of the transfer acceleration feature itself, any requests, such as GET or PUT to the bucket, **must** use this *new* transfer acceleration endpoint.

One final point to make with transfer acceleration is that there are a couple of S3 operations that it does not support, these being: 
- GET Service (list buckets)
- PUT Bucket (create bucket)
- DELETE Bucket
- Cross region copies using PUT Object - Copy.