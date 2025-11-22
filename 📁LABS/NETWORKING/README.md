 ### Networking Lab: Build Your VPC and Launch a Web Server
 
### Objective
-  Create VPC, subnets, configure security groups and launch an EC2 instance into a VPC
### Tasks
### Create your VPC
-  Created a new Virtual Private Cloud with a custom IPv4 CIDR block to provide an isolated network environment.
   ### Create additional subnets
-  Created a public subnet for resources that need internet access and a private subnet for internal resources. placed them in different availability zones to improve availability.
### Associate subnets and add routes
-  Associated the public subnet with a route table that connects to an internet gateway, and associated the private subnet with a route table without internet access for security.
### Create a VPC security group
- Created a security group allowing HTTP (port 80) from anywhere for web access
### Launch a web server instance
-  Deployed an EC2 instance in the public subnet, installed a web server, and confirmed that it was accessible in a browser.
### Challenges
- I forgot to assign public IP, the EC2 intance was not accessible
- Security group did not allow web traffic
### Takeaways
- Subnets must be associated with route tables.
### Screenshots
