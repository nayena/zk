# Amazon VPC


## Creating VPC using the wizard

- AWS will create a NAT instance. 
- The VPC has an implied router 
- Wizard updates the main route table used with the private subnet
- Wizard creates a custom route table and associates it with the public subnet


## Public Subnets

Within the public subnet, a public IP is essentially used for external traffic to communicate with your AWS resources and vice-versa.

Alternatives to public IPs are Internet Gateways, network ACLs and Customer Gateways.