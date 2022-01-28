# Amazon EC2

EC2 instances can be protected with Security Groups and these should, for all intents and purposes, be considered a virtual firewall to control traffic on one or more instances.


## Storage

There are typically three different types of storage you should think about, when using EC2.

- [[Amazon S3]] for objects where you write once and read many times, such as video files, images, static websites, and backup archives.
- [[Amazon Elastic Block Store]] is optimized for for low latency access and when fast, concurrent read and write operations are needed. This is persistent, meaning it will persist even if the underlying EC2 instance is stopped or terminated. Typically used like a regular hard drive.
- [[Amazon Elastic File System]] can be used by multiple servers at once.



EC2 instances can have either [[Amazon Elastic Block Store]] volumes attached *or* instance volumes attached.

For instance volumes, these are volumes that comes pre-defined with the servers and these have a few gotchas. Data can be lost on the volumes if:

- The underlying disk drive fails
- The instance stops
- The instance terminates

If the instance **reboots** (either intentionally or unintentionally) the data persists.