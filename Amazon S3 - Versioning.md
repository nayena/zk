# S3 Versioning

This allows multiple versions of a file to exist.

This allows for multiple versions of the same object to exist. This is useful to allow you to retrieve previous versions of a file, or recover a file should it subjected to *accidental deletion*, or *intended malicious* deletion of an object.

Within S3, there are three states of versioning:
- Unversioned (which is the default)
- Versioning-Enabled
- Versioning-Suspended


With versioning enabled you should also bear in mind that **you will incur additional storage costs** as you will be storing multiple versions of the same file, and one of the costing metrics of S3 is how much data storage you use.

Versioning can be enabled in the AWS console or via the CLI. It can either be configured during creation of the bucket or enabling it on an existing bucket.

For any new objects that are uploaded AFTER versioning has been enabled, the object will receive a new *Version ID*. 

If you enabled versioning on an existing bucket with objects already in them, then their ‘Version ID’ will be displayed as *null* until they have been modified or deleted. At which point they will receive a new Version ID.

If a versioned object is deleted, it receives a delete marker (and will generate a 404 if a GET call is issued), but all previous versions still exists.