# Amazon S3

All objects are **immutable**!

Individual files can at smallest be **0 bytes** and at largest **5TB**.

S3 is a **regional** service, which means you have to define where you want your data stored.

S3 has **eleven nines of durability**, means that your files are extremely durable, while the uptime of the service is between 99.5% and 99.9%. 

To store objects in S3, you need to create a bucket that is **globally unique** - but also DNS-compliant - due to the flat address space used in S3.

Features in S3, typically works at *a bucket level* and **not** at a folder level.


There are many advanced features in S3, these are:
- [[Amazon S3 - Versioning]]
- [[Amazon S3 - Server-Access Logging]]
- [[Amazon S3 - Static Website Hosting]]
- [[Amazon S3 - Object Level Logging]]
- [[Amazon S3 - Default Encryption]]
- [[Amazon S3 - Object Lock]]
- [[Amazon S3 - Transfer Acceleration]]
- [[Amazon S3 - Events]]
- [[Amazon S3 - Requester Pays]]

Additionally, several more features are available:

- Access Control Lists. These allow you to control which user or AWS account can access a Bucket or object, using a range of permissions, such as read, write, or full control, et cetera.
- Lifecycle Policies. Lifecycle Policies allow you to automatically manage and move data between classes, allowing specific data to be relocated based on compliance and governance controls you might have in place.
- MFA Delete. Multi-Factor Authentication Delete ensures that a user has to enter a 6 digit MFA code to delete an object, which prevents accidental deletion due to human error.

## Cross Region Replication
By enabling Cross Region Replication, you can maintain compliance whilst at the same time still have the data in the local region for optimum data retrieval latency.

You will be charged of COPY and PUT requests and only the storage cost.

## Multipart Uploading
Amazon recommends that for any file that you're trying to upload to S3, **larger than 100MB**, than you should implement **multipart** upload. This feature helps to increase the performance of the backup process.

As multiple parts can be uploaded at the same time in parallel, the speed and throughput of uploading can be enhanced.

Should there be any transmission issues or errors, it will **only affect the part being uploaded**, unaffecting the other parts. When this happens, only the affected part will need to be resent.

There is an element of management available whereby you can, if you're quiet, pause your uploads and then resume them at any point. Multipart uploads *do not have an expiry time*, allowing you to manage the upload of your data over a period of time.


## Storage Classes

### Standard
- Low Latency
- Frequent access to data
- Lifecycle rules can be configured
    - Automations can be configured, by moving data to cheaper storage classes after a certain amount of time
- Offers 99.99% availability

### Intelligent-Tiering
By selecting this one, S3 will analyze and move your data based on the usage pattern.
If an object isn't accessed within 30 days, it will be moved to the cheapest tier.

"only" offers 99.9% availability, which is one nine less than Standard

### Standard Infrequent Access
This can be seen as the equivalent to the infrequent tier from the Intelligent Tiering class as it is designed for data that does not need to be accessed as frequently as data within the Standard tier.

Availability is 99.9%

### One Zone Infrequent Access
Availability is 99.5%, due to only using a single AZ.

Not sure why anyone ever would use this.

### Glacier
This is intended for archival data and interacts directly with lifecycle rules as well.

The cost is a fraction of "regular" S3 storage. This comes at the cost of being significantly slower to get data out, usually minutes to hours.

When it comes to moving data into S3 Glacier for the first time it's effectively a two-step process. 
- Firstly, you need to create your vaults as your container for your archives and this could be completed using the Glacier console. 
- Secondly, you need to move your data into the Glacier vault using the available API or SDKs

There are three tiers to retrieve your data:

- Expedited. This is used when you have an *urgent* requirement to retrieve your data but the request has to be **less than 250 megabytes**. The data is then made available to you in **one to five minutes** and this is the most expensive retrieval option of the three.
- Standard. This can be used to retrieve any of your archives no matter their size but your data will be available in **three to five hours**, so much longer than the expedited option and this is the second most expensive of the three options.
- Bulk. This option is used to retrieve petabytes of data at a time, however, this typically takes between **five and twelve hours** to complete. This is the cheapest of the retrieval options so it really depends on how much data and how quickly you need it, as the retrieval speed and cost to be made by your retrieval option.

### S3 Glacier Deep Archive. 
This is the cheapest and again being a Glacier class, it focuses on long-term storage. 

This is an ideal storage class for circumstances that require specific data retention regulations and compliance with minimal access, such as those within the financial or health sector where data records might need to be legally retained for seven years or even longer.

The durability and availability matches that of S3 Glacier with eleven 9s durability across multiple AZs with 99.9% availability.

## Batch Operations
Batch operations allow you to carry out management operations across millions or even billions of your S3 Objects at the same time using a single API or by using the S3 Management Console.

Batch operations also integrate with AWS CloudTrail to monitor all changes made using the APIs selected. It also includes the ability to notify you when specific events occur and provide a completion report keeping you aware of the progress of your batch changes.

Being able to run huge batch management across your data storage in S3 can save you a huge amount of time by trying to develop other alternate methods in trying to achieve the same result. It’s also compatible with AWS Lambda, allowing you to run your functions across billions of objects at once.

## Glacier Select
Supports SQL type operations to retrieve specific types of data, which could save a lot of money.

## S3 Replication Time Control
S3-RTC is an advanced feature built on top of S3 replication that provides an SLA of ensuring that 99.9% of objects are replicated within 15 minutes of the start of the upload. 

This process can be monitored through the use of CloudWatch metrics (which are charged separately).