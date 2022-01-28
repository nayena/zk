# Amazon S3 - Events

Any events which are recorded can be sent to either an SNS Topic, an SQS Queue or a Lambda Function.

Selecting the Events tile from bucket properties screen enables you to configure which events are to be monitored.

You should give your event a descriptive name, followed by the required events that you want to monitor. There is quite a long list that can be monitored and captured within your bucket, i.e new objects, object removals, restores, RRS and replication events.

The *Prefix* element allows you to specify the events to be captured based on the objects prefix within the bucket, for example, you could capture all PUT, COPY and POST events for objects with a prefix of Logs/.

The *Suffix* provides a similar function of the prefix, it allows you to apply the event captures to objects with a certain suffix, for example all objects with a *.jpg file extension.

The *Send to* component determines where your events notifications will be sent, either to an SNS Topic, an SQS Queue or a Lambda Function.

Depending on the existing configurations of your destination of event notifications, permissions will need to be granted to your SNS Topic, SQS queue or Lambda function to enable S3 to publish events to them.