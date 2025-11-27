<img width="1536" height="1024" alt="Amazon EC2 Overview Illustration (1)" src="https://github.com/user-attachments/assets/90406d99-3fa6-49dc-a7e3-6dde5c125a00" />

`Amazon EC2 – Service Note (Summary)`
### 1. What is Amazon EC2?

- Amazon Elastic Compute Cloud (EC2) is a cloud service that provides secure, resizable virtual servers (instances) to run applications without managing physical hardware.

### 2. Key Features

- `Scalability`: Quickly increase or decrease compute capacity.

- `Instance Types`: General Purpose, Compute Optimized, Memory Optimized, Storage Optimized, and Accelerated Computing.

- `Elastic Block Store (EBS)`: Persistent storage volumes for EC2.

- `Security Groups`: Virtual firewalls that control inbound/outbound traffic.

- `Elastic IP`: Static public IP addresses for instances.

- `Elastic Load Balancing (ELB)`: Distributes traffic across multiple instances.

- `Auto Scaling`: Automatically adjusts the number of instances based on demand.

- `Pay-as-you-go Pricing`: Charged per second or hour depending on instance type.

### 3. Common Use Cases

- Hosting web applications

- Big data processing

- Running databases

- Containerized workloads

- Batch processing and analytics

- Development and test environments

### 4. Instance Lifecycle

- Launch

- Run

 - Stop/Start

- Hibernate (optional)

- Terminate

### 5. Storage Options

- `EBS Volumes`: Persistent, block-level storage

- `Instance Store`: Temporary, high-speed local storage

- `EFS`: Scalable file storage to share across multiple EC2

- `S3`: Object storage for backups, logs, images, etc.

### 6. Networking

- `VPC`: Isolated cloud network

- `Subnets`: Public and private networks

- `Security Groups`: Allow/deny traffic

- `Key Pairs`: SSH access security

### 7. Pricing Models

- `On-Demand`: Pay per hour/second, no commitments

- `Reserved Instances`: 1–3 year commitment, lower cost

- `Savings Plans`: Flexible compute discount

- `Spot Instances`: Cheapest—use for flexible or fault-tolerant workloads

### 8. Best Practices

- Choose the right instance type for your workload

- Use Auto Scaling for high availability

- Implement least-privilege security with IAM roles

- Regularly snapshot EBS volumes

- Use Monitoring `(CloudWatch)` for performance and cost tracking

- Apply patches using Systems Manager
