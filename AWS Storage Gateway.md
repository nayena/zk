# AWS Storage Gateway
The Storage Gateway itself is a software appliance that can be stored within your own data center which allows integration between your on-premise storage and that of AWS. This connectivity can allow you scale your storage requirements both securely and cost efficiently.

The software appliance can be downloaded from AWS as a virtual machine which can then be installed on your VMware or Microsoft hypervisors.

Storage Gateway offers three different configuration options:

## File Gateways
File gateways allow you to securely store your files as objects within S3. Using as a type of file share which allows you mount on map drives to an S3 bucket as if the share was held locally on your own corporate network. When storing files using the file gateway they sent to S3 over HTTPS and are also encrypted with S3's own server side encryption SSE-S3.

In addition to this local a on-premise cache is also provisioned for accessing your most recently accessed files to optimize latency with also helps to reduce egress traffic costs. When your file gateway's first configured you must associate it with your S3 bucket which the gateway will then present as a NFS V.3 or V4.1 file system to your internal applications.

This allows you to view the bucket as a normal NFS file system, making it easy to mount as a drive on Linux or map a drive to it in Microsoft. Any files that are then written to these NFS file systems are stored in S3 as individual objects as a one to one mapping of files to objects.

## Volume Gateways
These can be configured as either a stored volume gateway or a cached volume gateway.

### Stored Volume Gateways
Volumes created and configured within the storage gateway are backed by Amazon S3 and are **mounted as iSCSI devices** that your applications can then communicate with.

During the volume creation, these are mapped to your on-premise storage devices which can either hold existing data or be a new disk. 

As data is written to these iSCSI devices the data is actually written to your local storage services such as your own NAS, SAN or DAS storage solution. However the storage gateway then asynchronously copies this data to Amazon S3 as EBS snapshots.

These are 1GiB - 16TiB and can hold up to 32 volumes. This is configured to a maximum of 512TiB.

### Cached Volume Gateways
Cached volume gateways are differed to stored volume gateways in that the primary data storage is actually Amazon S3 rather than your own local storage solution.

However cache volume gateways do utilize your local data storage as a buffer and the cache for recently accessed data to help maintain low latency, hence the name, Cache Volumes.

Again, during the creation of these volumes they are **presented as iSCSI volumes** which can be mounted by an application service. The volumes themselves are backed by the Amazon S3 infrastructure *as opposed to your local disks as seen in the stored volume gateway deployment.* 

As a part of this volume creation you must also select some local disks on-premise to act as your local cache and a buffer for data waiting to be uploaded to S3.

This buffer is used as a staging point for data that is waiting to be written to S3 and during the upload process, the data is encrypted using an SSL channel where the data is then encrypted within SSE S3. 

The limitations is slightly different with cache volume gateways in that each volume created can be up to 32TB in size with support for up to 32 volumes meaning a total storage capacity of 1024TB per cache volume gateway.

## Gateway Virtual Tape Library
This allows you again to back up your data to S3 from your own corporate data center but also leverage Amazon Glacier for data archiving. Virtual Tape Library is essentially a cloud based tape backup solution replacing physical components with virtual ones.

This functionality allows you to use your existing tape backup application infrastructure within AWS providing a more robust and secure backup and archiving solution. The solution itself is comprised of the following elements.

Storage Gateway. The gateway itself is configured as a tape gateway which as a capacity to hold 1500 virtual tapes.

- Virtual Tapes. These are a virtual equivalent to a physical backup tape cartridge which can by anything from 100 gig to two and a half terabytes in size. And any data stored on the virtual tapes are backed by AWS S3 and appear in the virtual tape library.
- Virtual Tape Library. VTL. As you may have guessed these are virtual equivalents to a tape library that contain your virtual tapes.
- Tape Drives. Every VTL comes with ten virtual tape drives which are presented to your backup applications is iSCSI devices.
- Media Changer. This is a virtual device that manages tapes to and from the tape drive to your VTL and again it's presented as an iSCSI device to your backup applications.
- Archive. This is equivalent to an off-site tape backup storage facility where you can archive tapes from your virtual tape library to Amazon Glacier which as we already know, is used as a cold storage solution. If retrieval of the tapes are required, storage gateway uses the standard retrieval option which can take between 3 - 5 hours to retrieve your data.