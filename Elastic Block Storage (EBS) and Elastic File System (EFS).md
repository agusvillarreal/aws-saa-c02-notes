## EBS Overview
Virtual disk in the cloud
Storage volumes you can attach to your EC2 instances
Mission critical 
1. Production Worloads
2. Highly Available
3. Scalable

TYPES:
General Purpose SSD (gp2)
Good for boot volumes or developmed

General Purpose SSD (gp3)
A balance of price and performance
High performance at a low cost
4 times faster than max throughput of gp2 volumes

Provisioned IOPS SSD (io1)
High performance > 16,000 IOPS

Provisioned IOPS SSD io2
Lastest generation 
Application that need high levels of durability 

Hard Disk not bboot volume
Throughput Optimized HDD (st1)
Low-Cost HDD volume
Big data, data warehouses, ETL, and log processing
Cost-effective way to store mountains of data

Cold HDD (SC1)
Lowest Cost Option
Colder data file server
lowest cost and performance is not a factor

| IOPS                                                                               | Throughput                                                             |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| Measures the number of read and write operations per second                        | Measures the number of bists read or written per second                |
| Importante metric for quick transactions, low-latency apps, transactional worloads | Important metric for large ddatasets, large I/O sizes, complex queries |
| The ability to action reads and write very quickly                                 | The ability to deal with large datasets                                |
| Choose Provisioned IOPS SSD (io1 or io2)                                           | Choose Throughput Optimized HDD (st1)                                                                       |

Highly available and scalable sotrage volumes you can attach to an EC2 instance

| gp2 General Purpose                              | gp3 General Purpose                                                                 | io1 Provisioned IOPS SSD                             | io2 Provisioned IOPS SSD                                                    |
| ------------------------------------------------ | ----------------------------------------------------------------------------------- | ---------------------------------------------------- | --------------------------------------------------- |
| Suitable for boot disks and general applications | Suitable for high peformance applications                                           | Suitable for OLTP and latency-sensitive applications | Suitable for OLTP and latency-sensitve applications |
| Up to 16,000 IOPS per volume                     | Predictable 3,000 IOPS baseline performance and 125 MiB/s regardless of volume size | 50 IOPS/GiB                                          | 500 IOPS/GiB                                        |
| Up to 99.9% durability                           | Up to 99.9% durability                                                              | Up to 64,000 IOPS per volume                         | Up to 64,000 IOPS per volume                        |
|                                                  |                                                                                     | High performance and most expensive                  | 99.999% durability                                  |
|                                                  |                                                                                     | Up to 99.9% durability                               | Latest generation Provisioned IOPS volume           |

| st1 Throughput Optimized                   | sc1 Cold HDD                          |
| ------------------------------------------ | ------------------------------------- |
| Suitable  for big data warehouses, and ETL | Max throughput of 250 MB/s per volume |
| Max throughput is 500 MB/s per volume      | Less frequently accessed data         |
| Cannot be a boot volume                    | Cannot be a boot volume               |
| Up to 99.9 durability                     | Lowest Cost                                      |

## Volumes and Snapshots
Volumes -> Exists EBS Virtual Hard disk minnmun 1 volume per EC2 instance, root volume
Snapshots -> S3, photo of the virtual/volume, point in time, incremental

- Consistent Snapshots
- Encrypted Snapshots
- Sharing Snapshots

EBS Volumes
1. Location: EBS volumes will always be in the same AZ as EC2
2. Resizing: Resize on the fly
3. Volume TYPE: Switch volume type

- Volumes exists on EBS, whereas snapshots exist on S3
- Snapshots are point-in-time photographs of volumes and are incremental in nature
- The first snapshot will take some time to create. For consistent snapshots, stop the instance and detach the volume.
- You can share snapshots between AWS accounts as well as between regions, but first you need to copy that snapshoot to the target region
- You can resize EBS volumes on the fly as well as changing the volume types

## Protecting EBS Volumes with encryption
#### Encrypted Volumes
- Data at rest is encrypted inside the volume
- All data in flight moving between the instance and the volume is encrypted
- All snapshots are encrypted
- All volumes created from the snapshot are encrypted

#### How to encrypt volumes
- Create a snapshot of the unencrypted root device volume
- Create a copy of the snapshot and select the encrypt option
- Create an AMI from the encrypted snapshot
- Use that AMI to launch new encrypted instances

## EC2 Hibernation
- EC2 hibernation preserves the in-memory RAM on persisten storage (EBS)
- Much faster to boot up because you do not need to reload the operating system
- Instance RAM must be less than 150 GB
- Instance families include C3, C4, C5, M3, M5, R3, R4 and R5
- Available for Windows, Amazon Linux 2, and Ubuntu
- Instances can't be hibernated for more that 60 days
- Available for On-demand instances and Reserved Instances

## EFS Overview
EFS-> network file system, ec2 instances in multiple availability zones, shared storage
**Supports** the Network File System version 4 (NFSv4) protocol
Only pay for the storage you use (no pre-previsioning required)
Can scale up to petabytes
Can **support** thounsands of concurrent NFS connections
Data is stored across multiple AZs within a region
Read-after-wirte consistency
**highly scalable shared storage using NFS**

## FSx Overview
Windows File server, managed native Microsoft windows file system
1. EFS: When you need distributed, highly resilient storage for Linux instances and Linux-based applications
2. Amazon FSx for Windows: When you need centralized storage for Windows-based applications, such as SharePoint, Microsoft SQL server, workspaces, IIS web server, or any other native Microsoft application
3. Amazon FSx for Lustre: When you need high-speed, high-capacity distributed storage. This will be for applications that do high performance computing (HPC), financial modeling, etc. Remembder that FSx for Lustre can store data directly on S3

## Amazon Machine Images: EBS vs Instance Store
AMI -> provides the information required to launch an instance

#### Instance Store Volumes
> Instance store volumes are sometimes called ephemeral storage. Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data. You can, however, reboot the instance without losing your data.
> If you delete the instance, you will lose the instance store volume

#### EBS volumes
> EBS-backed instances can be stopped. You will not lose the data on this instance if it is stopped. You can also reboot an EBS volume and not lose your data
> By default, the root device volume will be deleted on termination. However, you can tell AWS to keep the root device volume with EBS volumes

AMI is just a blueprint for an ec2 instance

## AWS Backup
- Consolidation: Use AWS Backu´to back up AWS services, such as EC2, EBS, EFS, Amazon FSx for Lustre, Amazon FSx for Windows File Server, and AWS Storage Gatewat
- Organizations: You can use AWS Organizations in conjuction with AWS Backup to back up your different AWS services across multiple AWS accounts
- Benefits: Backup gives you centralized control, letting you automate your bachups and define lifecycle policies for your data. You get better compliance, as you can enforce your backup policies, ensure your backups are encrypted, and audit them once complete


## Storage Options Use Cases
- S3
	- Used for serverless object storage
- Glacier
	- Used for archiving objects
- EFS
	- Network File System (NFS) for Linux instances. Centralized storage solution across multiple AZs
- FSx for Lustre
	- File storage for high performance computing Linux file systems
- EBS Volumes
	- Persistent storage for EC2 instances
- Instance Store
	- Ephemeral storage for EC2 instances
- FSx for Windows
	- File storage for Windows instances. Centralized storage solution across multiple AZs
