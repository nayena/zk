# Amazon FSx

Amazon FSx is another storage service that focuses on file systems, much like EFS. However, FSx comes in 2 forms, firstly Amazon FSx for Windows File Server, and also Amazon FSx for Lustre. 

Each FSx option has been designed for very different needs and requirements.

## Amazon FSx for Windows File Server 

It provides a fully managed native Microsoft Windows file system on AWS. You can easily move and migrate your windows-based workloads requiring file storage. The solution is built upon Windows Server, it operates as shared file storage. It has full support for: SMB protocol, Windows NTFS, Active Directory (AD) integration, and Distributed File System (DFS). 

It uses SSD storage for enhanced performance and throughput providing sub-millisecond latencies.

One benefit that you currently get with Amazon FSx for Windows File Server over Amazon FSx for Lustre is that of data deduplication. This can be activated for your file system and can save you up to 80% is storage costs depending on what data you are storing.

## Amazon FSx for Lustre
It is a fully managed file system designed for compute-intensive workloads, for example, Machine Learning and high-performance computing. It has the ability to process massive data sets. 

Performance can run up to hundreds of GB per second of throughput, millions of IOPS, and sub-millisecond latencies. It has integration with Amazon S3 and supports and supports cloud-bursting workloads from on-premises over Direct Connect and VPN connections.