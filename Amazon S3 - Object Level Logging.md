# Amazon S3 - Object Level Logging
This feature is actually more closely related to the [[AWS CloudTrail]] service than S3 in a way, as it’s AWS CloudTrail that performs logging activities against Amazon S3 data events. These data events are specific API calls used in S3, such as `GetObject`, `DeleteObject`, and `PutObject`.

When an API request is initiated, AWS CloudTrail captures the request as an event and records this event within a log file which is then stored on S3.

Each API call represents a new event within the log file. CloudTrail also records and associates other identifying metadata with all the events. For example, the identity of the caller, the timestamp of when the request was initiated and the source IP address.