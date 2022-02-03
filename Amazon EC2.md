# Amazon EC2

EC2 instances can be protected with Security Groups and these should, for all intents and purposes, be considered a virtual firewall to control traffic on one or more instances.


## Storage

There are typically three different types of storage you should think about, when using EC2.

- [[Amazon S3]] for objects where you write once and read many times, such as video files, images, static websites, and backup archives.
- [[Amazon Elastic Block Store]] is optimized for for low latency access and when fast, concurrent read and write operations are needed. This is persistent, meaning it will persist even if the underlying EC2 instance is stopped or terminated. Typically used like a regular hard drive.
- [[Amazon Elastic File System]] can be used by multiple servers at once.

EC2 instances can have either [[Amazon Elastic Block Store]] volumes attached *or* instance volumes attached.

EC2 instances can also have ephemeral storage attached. This is considered temporary and data will be lost if the instance is stopped or terminated. This cannot be detached from the instance.

For instance volumes, these are volumes that comes pre-defined with the servers and these have a few gotchas. Data can be lost on the volumes if:

- The underlying disk drive fails
- The instance stops
- The instance terminates

If the instance **reboots** (either intentionally or unintentionally) the data persists.

## AMIs (Amazon Machine Images)
These are essentially templates of pre-configured EC2 instances which allow you to quickly launch a new EC2 instance based on the configuration within the AMI.

From a high level perspective an AMI is an image baseline that will include an operating system and applications along with any custom configuration.

## Instance Types
When picking an instance type, there are a bunch of variables. These are:

An instance type simply defines the size of the instance based on a number of different parameters, these being 

- ECUs - this defines a number of EC2 compute units for instance, 
- vCPUs this is the number of virtual CPUs on the instance. 
- Physical processor, this is the process speed used on the instance. 
- Clock speed, it's clock speed in gigahertz. 
- Memory, the amount of memory associated. 
- Instance storage this is the capacity of the local instance store volumes available. 
- EBS optimized available, this defines if the instance supports EBS optimized storage or not. 
- Network performance, this shows the performance level of rate of data transfer. 
- IPV6 support, this simply indicates if the instance type supports IPV6. 
- Process architecture this shows the architected type of the processor. 
- AES-NI, this stands for advanced encryption standard new instructions and it shows if the instance supports it for enhanced data protection. 
- AVX this indicates if the instance supports AVX which is advanced vector extensions, which are primary used for applications focused on audio and video, scientific calculations and 3D modeling analysis. 
- Turbo which shows if the instance supports intel turbo boost and AMD turbo core technologies

## Instance Families
- Micro instances, these instances have a low cost against them due to the minimal amount of CPU and memory power that they offer. These are ideal for very low throughput use cases such as low traffic websites.
- General-purpose, instance types within this family have a balanced mix of CPU memory and storage making them ideal for small to medium databases, tests and development servers and back-end servers.
- Compute optimized, as the name implies instance types within this family have a greater focus on compute. They have the highest performing processes installed allowing them to be used for high-performance front end servers, web servers, high-performance science and engineering applications and video encoding and batch processing. 
- GPU, GPU stands for graphics processing unit. And so the instances within this family are optimized for graphic intensive applications. 
- FPGA, this family of instances allows you to customize field programmable gate arrays. To create application specific hardware accelerations when used with applications that use massively parallel processing power such as genomics and financial computing.
- Memory optimized, this family include instance types that are primarily used for large-scale enterprise class in-memory applications, such as performing real time processing of unstructured data. They are also ideal for enterprise applications such as Microsoft SharePoint. These instances of the lowest cost per gigabyte of RAM against all other instance families. 
- Storage optimized, as expected these are optimized for enhanced storage. Instances in this family use SSD backed instant storage for low latency and very high I/O, input/output performance, including very high IOPS which is input/output operations per second. And these are great for analytic workloads and no SQL databases. Data file systems and log processing applications.

## Purchasing Options
The different EC2 payment options are as follows: 
- on-demand instances
    - 
- reserved instances
    - Reserved instances allow you to purchase a discount for an incidents type with set criteria for a set period of time in return for a reduced cost compared to on-demand instances. This reduction can be as much as 75%. These reservations against instances must be purchased in either one or three year time frames.
    - Used for **long-term** *predicable* workloads.
- scheduled instances
    - These are similar to reserved instances and the fact that you pay for the reservations of an instance on a recurring schedule, either daily, weekly or monthly. For example you might have a weekly task that is scheduled that performs some kind of bulk processing for a number of hours at the same time every week.
- spot instances
    - bidding, based on unused resources
- on-demand capacity reservations.
    - This allows you to reserve capacity for your EC2 instances based on different attributes. Such as instance type, platform and tenancy et cetera. Within a particular availability zone for any period of time. This ensures that you always have the available number of instances you require within a specific availability zone immediately.

## Tenancy
Shared Tenancy means that the same host may be used by multiple customers. Security mechanisms are in place to protect VMs.

Dedicated Instances are run on hardware that no other customer can access. This may be for compliance reasons. **Dedicates instances incur additional charges.**

Dedicated Hosts means you have additional control over the physical host.

## User Data
This is where you put in a script that will be run on boot. Like bootstrapping itself.