### Summary: Networking Service Note
<img width="1280" height="617" alt="image" src="https://github.com/user-attachments/assets/958cd251-cd97-4008-85f5-b9dce13c4d1c" />

### 1. What Are AWS Networking Services?

- AWS Networking services allow you to build secure, scalable, and reliable network environments in the cloud. They help control traffic, connect resources, and integrate on-premises networks with AWS.

### 2. Key Networking Components
✔ Amazon VPC (Virtual Private Cloud)

- Your isolated cloud network where you define IP ranges, subnets, routing, and security.

### ✔ Subnets (Public & Private)

- Public: Resources accessible from the internet.

### Private: Internal-only resources.

### ✔ Security Groups

- Instance-level firewall that controls inbound and outbound traffic.

### ✔ Network ACLs (NACLs)

- Subnet-level firewall offering stateless traffic filtering.

### ✔ Internet Gateway (IGW)

- Allows communication between VPC resources and the internet.

#### ✔ NAT Gateway / NAT Instance

-Enables private resources to access the internet securely.

### ✔ Route Tables

- Define how traffic is directed within subnets and outside the VPC.

### ✔ Elastic Load Balancers (ELB)

- Distribute traffic across multiple servers to improve availability.

### ✔ Amazon Route 53

- DNS service for domains, routing, and health checks.

### ✔ VPC Peering / Transit Gateway

- Connect VPCs across regions or accounts at scale.

### ✔ AWS Direct Connect

- Provides a dedicated, private link from your data center to AWS.

### 3. Common Use Cases

- Hosting secure applications

- Building hybrid cloud environments

- Managing network segmentation

- Handling large-scale routing

- Load balancing web traffic

### 4. Benefits

- Highly secure, layered protection

- Scalable and customizable

- Low-latency, high-performance networking

- Supports hybrid and multi-cloud architectures

- Pay-as-you-use
