# Amazon Elastic Block Store
Also known as EBS.

Primarily used for rapidly changing data.

EBS Offers to do point-in-time backups, also known as snapshots. Can be manually invoked or automated using Amazon CloudWatch Events.

These snapshots are incremental and a new volume can be created from any snapshot.

It is possible to copy snapshots from one region to another.

The EBS volume itself is only available inside the AZ that it was created in.

## Volume Types
### General Purpose SSD (GP2)
SSD backed storage is suited for scenarios that work with smaller blocks. Such as databases using transactional workloads.

Often used as boot volumes for EC2 instances.


### Provisioned IOPS SSD (IO1)
Provisioned IOPS SSD volumes deliver enhanced predictable performance for applications requiring I/O intensive workloads. They also have the ability to specify IOPS rate during the creation of a new EBS volume.

And the volumes range from *four to sixteen terabytes* in size.

Per volume, the maximum IOPS possible is set to **20,000 IOPS**.

### Cold HDD (SC1)
The cold HDD offers the lowest cost of all EBS volumes. These volumes are suited for large workloads, but those that are **accessed infrequently**. The HDD does have capacity to burst up to significant speeds.

These volumes cannot be used for boot disks.

### Throughput Optimized HDD (ST1)
The "warm" HDD are designed for frequently accessed data and are ideally suited to work well with large data sets requiring throughput-intensive workloads, such as data streaming, big data, and log processing.

These volumes cannot be used for boot disks.

## Security
Enabling volume encryption is done by filling out a checkbox. Encryption is done with AES-256 and provides its encryption process by using another AWS service, KMS, which uses Customer Master Keys.

A default region setting can be enabled.

## Creating the volumes
When creating a volume as a standalone, you can decice whether to create it from a blank slate or from a snapshot.

## Resizing
Can be done elastically via either the console or the CLI.
Can also be done by creating a snapshot of the existing volume and then creating a new volume from that snapshot with increased size.

## When not to use
- For temp storage
- For multi-instance access
- For very high durability and availability