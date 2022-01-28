# Amazon S3 - Static Website Hosting

If you are looking to create a simple and static website that requires no server-side scripting of any kind, then this can easily be hosted with one of your Amazon S3 buckets.

There are a few gotchas:
- This does not it does not support HTTPS requests. 
- The bucket and its contents must be marked as publicly accessible.
- It does not support Requester Pays

Advanced redirection rules can be configured and this is done with fancy XML or in JSON. See more at https://docs.aws.amazon.com/AmazonS3/latest/userguide/how-to-page-redirect.html#advanced-conditional-redirects

You can also use this to redirect websites. One common use-case is to redirect www to non-www sites.

All objects in the bucket needs to have the `s3:GetObject` option. It must also contain an index.html file.