# Amazon Backup
AWS Backup acts as a central hub to manage backups across your environment, across multiple regions, centralizing management and providing full auditability in addition to assisting with specific compliance controls. 

Having a managed service monitor and control your backups allows for all logging to be consolidated in a single place, in addition to seeing the status of completed backups and perform and restores required.

The service itself uses backup features from existing services, so for example, if you were to manage your EBS backups, AWS Backup would manage these through the EBS Snapshot feature as a way of performing the backup.

When using AWS Backup you will need to create backup policies or backup plans. These simply determine the exact requirements that you need for your backups and contain information such as:

- A backup schedule
- Backup window
- Lifecycle rules, such as the transition of data to cold storage after a set period
- A backup vault, which is where your backups are stored and encrypted through the use of KMS encryption keys
- Regional copies
- Tags