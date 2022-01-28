# Amazon Elastic File System

EFS is a fully managed, highly available and durable service that allows you to create shared file systems that can easily scale to petabytes in size with low latency access. It uses standard operating system APIs, so any application that is designed to work with standard operating system APIs will work with EFS.

It supports both NFS versions 4.1 and 4.0, and uses standard file system semantics such as strong consistency and file locking. It's replicated across availability zones in a single region making EFS a highly reliable storage service.

Much like traditional file servers, or a SAN or a NAS, Amazon EFS provides the ability for users to browse cloud network resources. 

EC2 instances can be configured to access Amazon EFS using configured mount points. 

Mount points can be created in multiple availability zones that attach to multiple EC2 instances.

At this point in time, Windows Operating System **does not support** EFS.

## Permissions
To create EFS resources, you need the following permissions:
- `elasticfilesystem:CreateFileSystem`
- `elasticfilesystem:CreateMountTarget`
- `ec2:DescribeSubnet`
- `ec2:CreateNetworkInterface`
- `ec2:DescribeNetworkInterfaces`

If you want to manage EFS via the AWS Console, you additionally need the following:
- `ec2:DescribeAvailabilityZones`
- `ec2:DescribeSecurityGroups`
- `ec2:DescribeVpcs`
- `ec2:DescribeVpcAttribute`
- `kms:ListAliases
- `kms:DescribeKey`

## Encryption

### At Rest
This uses another AWS service, the key management service known as KMS, to manage your encryption keys. 

A customer master key is the main key type within KMS. This key can encrypt data of up to four kilobytes in size, however, it is typically used in relation to your data encryption keys. 

The CMK can generate, encrypt, and decrypt these data encryption keys, which are then used outside of the KMS service by other AWS services to perform encryption against your data, for example, EFS. 

It's important to understand there are **two** types of customer master keys. 
- Those which are managed and created by customers of AWS, which can either be created using KMS, or by importing key material from existing key management applications into a new CMK.
- Those that are managed and created by AWS themselves. 

These AWS managed keys can only be used by the corresponding AWS service that created them within the particular region, as KMS is a regional service. These CMKs that are used by the services are generally created the first time you implement encryption using that particular service.

### In Transit
If you need to ensure your data remains secure between the EFS file system and your end client, then you need to implement encryption in transit.

The encryption is enabled through the utilization of the TLS protocol, which is transport layer security, when you perform your mounting of your EFS file system. 

The mount helper, offers a simple option `-o tls` to enable TLS v1.2

## Importing data into AWS EFS
The recommended course of action is to use another service called AWS DataSync. 

The data transfer can either be accomplished over a direct connect link or over the internet. 
To sync source files from your on-premises environment, you must download the DataSync agent as a VMware ESXi host to your site. The agent is configured with the source and destination target and associated with your AWS account, and logically sits in between your on-premise file system and your EFS file system.

These are some use-cases: 
- You can migrate an NFS file system from Amazon EC2 to Amazon EFS within the same AWS region.
- Replace an NFS file system from Amazon EC2 in one AWS region to an Amazon EFS file system in a different AWS region for disaster recovery.
- You can migrate an Amazon EFS file system from EFS standard with no lifecycle management to an EFS file system with lifecycle management enabled.
- You can migrate an Amazon EFS file system from one performance mode to another performance mode within the same AWS region.
- Replicate an Amazon EFS file system from one AWS region to another Amazon EFS file system in a different AWS region for disaster recovery.

## Storage Classes

### Standard
You are only charged based on amount of storage used per month.


### Infrequent Access (IA)
This comes at a cheaper price, meaning there is a latency impact and should only be used for infrequently accessed things. IA charges for both reads and writes.

## Lifecycle management
EFS can move files into IA, just like S3 to optimize costs. Options for this is 14, 30, 60, or 90 days. This can only be done for files larger than 128K and not for metadata.

## Performance Modes

There is a metric in CloudWatch to monitor the IOPS and how close you are to the 7K limit.

### General Purpose
This is the default and should be used for most use-cases. Offers good throughput with low latency, but is limited to 7K IOPS.
### Max I/O
Should you need more than 7K IOPS, this mode is better suited. The downside is, however, that your file operation latency will take a negative hit over that of General Purpose.

## Throughput Modes
These are measured in mebibytes per second (MiB/S)

### Bursting Throughput
This is the default mode and the amount of throughput scales as your file system grows. 

The default throughput available is capable of bursting to 100 mebibytes per second, however, with the standard storage class, this can burst to 100 mebibytes per second per tebibyte of storage used within the file system.

This is managed by earning credits, which happens when below the baseline burst. These credits can be used to boost above the burst limits. If you often reach this limit, you should consider using provisioned throughput.

### Provisioned Throughput
This allows you to mix and match. Say 500MiB/S for 1TB.
