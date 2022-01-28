# Amazon S3

All objects are **immutable**!

Individual files can at smallest be **0 bytes** and at largest **5TB**.

S3 is a **regional** service, which means you have to define where you want your data stored.

S3 has **eleven nines of durability**, means that your files are extremely durable, while the uptime of the service is between 99.5% and 99.9%. 

To store objects in S3, you need to create a bucket that is **globally unique** - but also DNS-compliant - due to the flat address space used in S3.

Features in S3, typically works at *a bucket level* and **not** at a folder level.

## Storage Classes

### Standard
- Low Latency
- Frequent access to data
- Lifecycle rules can be configured
    - Automations can be configured, by moving data to cheaper storage classes after a certain amount of time
- Offers 99.99% availability

### Intelligent-Tiering
By selecting this one, S3 will analyze and move your data based on the usage pattern.
If an object isn't accessed within 30 days, it will be moved to the cheapest tier.

"only" offers 99.9% availability, which is one nine less than Standard

### Standard Infrequent Access
This can be seen as the equivalent to the infrequent tier from the Intelligent Tiering class as it is designed for data that does not need to be accessed as frequently as data within the Standard tier.

Availability is 99.9%

### One Zone Infrequent Access
Availability is 99.5%, due to only using a single AZ.

Not sure why anyone ever would use this.

### Glacier
This is intended for archival data and interacts directly with lifecycle rules as well.

The cost is a fraction of "regular" S3 storage. This comes at the cost of being significantly slower to get data out, usually minutes to hours.

When it comes to moving data into S3 Glacier for the first time it's effectively a two-step process. 
- Firstly, you need to create your vaults as your container for your archives and this could be completed using the Glacier console. 
- Secondly, you need to move your data into the Glacier vault using the available API or SDKs

There are three tiers to retrieve your data:

- Expedited. This is used when you have an *urgent* requirement to retrieve your data but the request has to be **less than 250 megabytes**. The data is then made available to you in **one to five minutes** and this is the most expensive retrieval option of the three.
- Standard. This can be used to retrieve any of your archives no matter their size but your data will be available in **three to five hours**, so much longer than the expedited option and this is the second most expensive of the three options.
- Bulk. This option is used to retrieve petabytes of data at a time, however, this typically takes between **five and twelve hours** to complete. This is the cheapest of the retrieval options so it really depends on how much data and how quickly you need it, as the retrieval speed and cost to be made by your retrieval option.

### S3 Glacier Deep Archive. 
This is the cheapest and again being a Glacier class, it focuses on long-term storage. 

This is an ideal storage class for circumstances that require specific data retention regulations and compliance with minimal access, such as those within the financial or health sector where data records might need to be legally retained for seven years or even longer.

The durability and availability matches that of S3 Glacier with eleven 9s durability across multiple AZs with 99.9% availability.