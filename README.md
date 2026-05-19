**AWS Secure Cloud Architecture — Defense in Depth**
This repository contains the architecture pattern and configuration blueprints for a highly secure, resilient, and multi-tiered AWS infrastructure. 

**Architecture Overview**
The architecture isolates components into distinct network layers (subnets) based on their function and exposure risk, ensuring that a breach at any single layer does not compromise the entire system.

Key Architectural Layers
1. Edge & Network Perimeter (Public Subnet)
•	Internet Gateway (IGW): Handles public IP mapping and NAT for external internet traffic.
•	Application Load Balancer (ALB): * Internet-facing, listening exclusively on HTTP:80 (can be upgraded to HTTPS:443).

NAT Gateway: Deployed in the public subnet to allow instances in the private subnet to securely fetch software updates and communicate with AWS Systems Manager (SSM) without exposing them to inbound internet traffic.

2. Application Layer (App Private Subnet)
•	Network Isolation: Has no direct internet route.
•	Compute: Features EC2 Instance A (AZ-a) and EC2 Instance B (AZ-b) deployed across two Availability Zones for high availability.
•	Auto Scaling Group (ASG): Configured with min:2 and max:4 instances, utilizing Elastic Load Balancing (ELB) health checks to automatically replace unhealthy instances.
•	Security Configuration: * No public IPs assigned to EC2 instances.

3. Data & Storage Layer (Data Private Subnet)
•	Network Isolation: Maximum isolation with no internet route and no NAT gateway access.
•	Database: Amazon RDS MySQL instance protected by data-sg.
•	Secrets Management: Integrated with AWS Secrets Manager to handle database credentials.


