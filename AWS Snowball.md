# AWS Snowball
The AWS Snowball service, whereby AWS will send you an appliance, either 50 TB or 80 TB in size, to your data center, where you can then copy your data to it before it is shipped back to AWS for uploading onto S3. You can use multiple Snowballs at a time to transfer Petabytes of data if required.

The appliance is dust, water, and tamper resistant and can even withstand a eight and a half G jolt from within it's own external shipping container.

The snowball appliance has been designed to allow for high speed data transfer, thanks to a range of interfaces allowing you to select the most appropriate connection for your needs.

Onboard the snowball appliance, the following I/O 10-gigabit interfaces are available:
- RJ45 using Cat6
- SFP+ Copper
- SFP+ Optical

By default, all data transferred to the snowball appliance is automatically encrypted using 256-bit encryption keys generated from KMS, the key management service. 

Whilst on the topic of security, it also features end to end tracking using an E-ink shipping label. This ensures that when the device leaves your premises, it is sent to the right AWS facility.

As a general rule, if your data retrieval will take **longer than a week** using your existing connection method, then you should consider using AWS Snowball.