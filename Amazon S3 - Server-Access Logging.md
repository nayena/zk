# Amazon S3 - Server-Access Logging

When server-access logging is enabled on a bucket, it captures *details of requests that are made to that bucket and its objects*. Server-access logging, is **not guaranteed** and is conducted on a **best-effort basis by S3**.

To allow S3 to write access logs to a target bucket, it will, of course, require specific permissions. These permissions will require *write access* for a group known as the **Log Delivery** group, which is a pre-defined Amazon S3 group used to deliver log files to your target buckets.


These are gotchas with Access Logging:
- Firstly, both the source and target buckets should be in the same region, and it’s a best practice that different buckets are used for each. 
- The permissions of the S3 Access Log Group can **only** be assigned via Access Control Lists and not through bucket policies, so when manually setting the permissions for this via an SDK, you must update the ACL.
- If you have encryption enabled on your target bucket, access logs will **only** be delivered if this is set to SSE-S3 (Server-side encryption managed by S3) as **encryption with KMS is not supported**.


## Content of logs
Similar to a nginx http log, here are what each line contains:
- Bucket owner - Represents the canonical user ID of the owner of the Source bucket. The canonical user ID is used for cross-account access via bucket policies.
- Bucket - This shows the name of the bucket related to the request.
- Time - This is a timestamp of the request in UTC (Coordinated Universal Time).
- Remote IP Address - Represents the internet address of the identity carrying out the request.
- Requester - For authenticated users, this field will show the IAM identity. For any unauthenticated users a hyphen (-) would be displayed instead.
- Request ID - A random string to identify each request.
- Operation - This will display the operation of the request that was carried out.
- Key - The "key" part of the request, URL encoded, or if no key parameter is used then a hyphen will be displayed as in this example. A hyphen in any field of the request indicates that the available data was not known or was not applicable for the request.
- Request URI - This represents the Request-URI element of the HTTP request.
- HTTP Status - This displays the HTTP status returned from the request as a numeric value.
- Error Code - If an error was experienced, then S3 will return the error code received.
- Bytes Sent - The number of bytes sent as a response.
- Object Size - The size of the object in question in the request.
- Total Time: - Measured in milliseconds, it represents how long the request took from receiving the request to the last byte of sending a response.
- Turn-Around Time - This shows how long it took S3 to process the request.
- Referer - The value is taken from the HTTP referer header, however, in this case, there was none present and so a hyphen is represented as the value.
- User-Agent - This shows the value taken from the HTTP user-agent header.
- Version ID - If present, this will show the Version ID of the request.
- Host Id - The x-amz-id-2 or Amazon S3 extended request ID. The x-amz-id-2 header is a token that is used together with the x-amz-request-id header to help AWS troubleshoot problems.
- Signature Version - This will show which signature version was used to authenticate the request.
- Cipher Suite - If SSL was used it will show which cipher suite was used. If HTTP was used, then a hyphen would be shown instead.
- Authentication Type - This shows the type of authentication used for the request.
- Host Header - Represents the endpoints used to connect to Amazon S3 in the request.
- TLS Version - This shows which version of TLS was used by the client.