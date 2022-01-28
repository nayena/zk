# Business Continuity Plan

A company typically decides on an acceptable business continuity plan based on the financial impact to the business when systems are unavailable. 

The company determines the financial impact by considering many factors, such as the loss of business and the damage to its reputation due to downtime or the lack of systems availability.

## Recovery Time Objective 
The RTO is the time it takes after a disruption to restore a business process to its service level as was defined by the operational level agreement. 

For example, if a disaster occurs at 12:00 and the RTO is eight hours, then the disaster recovery process should restore the business process to the acceptable service level by 20:00.

## Recovery Point Objective
The RPO is the acceptable amount of data loss measured in time.

It is also a time value, but it's a slightly different one. RPO and RTO are two are quite different concepts. 

This is defined as the acceptable amount of data loss measured in time. For example, if that disaster occurred at 12 o'clock around lunchtime and the RPO is one hour, the system should recover all data that was in the system before 11:00. So the data loss will only account for one hour between 11:00 and 12:00.

# Strategies
### Backup & Restore
This is the concept of ensuring continously created backups and simply restoring a backup, to ensure a minimum amount of data loss.

To ensure that this works, a retention policy must be defined and followed. This is usually a requirement in many different compliance frameworks.

Regular tests must be carried out, to ensure that the process works.

### Pilot Light
This describes making sure that data is replicated from one region to another and then making sure that services (like servers, functions or other things) can be created rapidly, i.e using templating (terraform or cloudformation).

As with the backup&restore strategy, this must also regularly be tested.

This method relies on much heavier automation.

### Warm Standby
This method relies on having a cloned production environment, that is configured with a minimal footprint (no HA and similar). This should be as close to production as possible.

Recovery is swift, as the environment only needs to be scaled up.

### Multi-site
This is similar to the Warm Standby method, only where it is a 1:1 clone of production. Traffic should be sent to both environments, so they both are in use at all times. In case of failure, automation should be take place to route traffic to the non-failing environments.