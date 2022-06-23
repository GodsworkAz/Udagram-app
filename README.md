# Udagram App

Udagram App is an Instagram clone. This Cloudformation script builds the necessary infrastructure for the application:

The main infrastructure is built using two stacks: network stack and server stack.

### Network stack
The network stack does the following:
- Creates a VPC
- Creates 2 public subnets and 2 private subnets inside the VPC. The public and private subnets are spread across two availability zones in the region
- Launches NAT gateways in both public subnets
- Creates Elastic IPs for the NAT gateways
- Setup a public route table, attaches an internet gateway to it
- Associate the public subnet with the public route table 
- Setup 2 private route table, 1 per NAT gateway and associate the private subnets
- Outputs and exports the VPC ID, public and private subnet ID

### Server stack

This cloudformation script creates the resources for the Udagram application
- Creates a launch configuration
- Creates an auto-scaling group (minimum of 4 and maximum of 5 instances)
- Creates security groups to allow http
- Create instance profile and IAM role for S3 Read access. Associate the instance profile with the instances (not implemented in this commit)
- Bastion host not implemented in this commit
- Creates a Load balancer


Run the create cloudformation script in BASH:
> `cloudformation.sh`

This will create both stacks by running two _create.sh_ commands
