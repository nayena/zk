# Amazon EC2

EC2 instances can be protected with Security Groups and these should, for all intents and purposes, be considered a virtual firewall to control traffic on one or more instances.


## Storage
EC2 instances can have either [[Amazon Elastic Block Store]] volumes attached *or* instance volumes attached.

For instance volumes, these are volumes that comes pre-defined with the servers and these have a few gotchas. Data can be lost on the volumes if:

- The underlying disk drive fails
- The instance stops
- The instance terminates

If the instance **reboots** (either intentionally or unintentionally) the data persists.