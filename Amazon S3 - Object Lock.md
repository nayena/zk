# Amazon S3 - Object Lock
This feature is often used to meet a level of compliance known as WORM, meaning Write Once Read Many. 

It allows you to offer a level of protection against your objects in your bucket and prevents them from being deleted, either for a set period of time that is defined by you or alternatively prevents it from being deleted until the end of time! 

The ability to add retention periods using Object Lock help S3 to comply with regulations such as FINRA, the Financial Industry Regulatory Authority.

Setting Object Lock on a bucket can only be achieved **at the time of the creation of the bucket**. Once you have created your bucket with object lock enabled it will be **permanently enabled and can’t be disabled**.

Two retention modes exist for two different compliance requirements and they are as follows:

## Governance Mode
This prevents your users from performing a delete or an overwrite of any of the versions of your objects in the bucket throughout the duration set by the retention period. 

However, if you have very specific permissions, including `s3:BypassGovernanceMode`, `s3:GetObjectLockConfiguration`, `s3:GetObjectRetention`, then a user will still be able to delete an object version within the retention period or change any retention settings set on the bucket.

## Compliance Mode
The key difference between Compliance Mode and Governance Mode is that there are **NO** users that can override the retention periods set or delete an object, and **that also includes your AWS root account** which has the highest privileges. 

Essentially, any object added to a bucket configured for Compliance Mode means that the object will remain for the duration of the retention period.

## Legal Hold
The legal hold element only appears for object versions and not at the bucket level and acts much like a retention period and prevents the object from being deleted, however, legal holds do not have an expiration date.

Therefore, the object will remain protected until a user with permissions of `s3:PutObjectLegalHold` disables the legal hold on the object.

If an object is already protected by a retention period, a legal hold can also be placed on the object. When the retention period expires, the object will still be protected by the legal hold regardless of the fact that the retention period has expired.