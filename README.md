**AWS Secure Cloud Architecture — Defense in Depth**
This repository contains the architecture pattern and configuration blueprints for a highly secure, resilient, and multi-tiered AWS infrastructure. 

**Architecture Overview**
The architecture isolates components into distinct network layers (subnets) based on their function and exposure risk, ensuring that a breach at any single layer does not compromise the entire system.

       [ Internet ]
            │
            ▼
   [ Internet Gateway ]
            │
    ┌───────┴──────────────────────────────────┐
    ▼ (Public Subnet)                          ▼ (Public Subnet)
[ Application Load Balancer ]           [ NAT Gateway (Outbound Only) ]
    │                                          ▲
    ├──────────────────────┐                   │ (Outbound SSM/Updates)
    ▼ (Private App Subnet)  ▼ (Private App Subnet) │
[ EC2 Instance A ]      [ EC2 Instance B ] ────┘
    │ (Port 3306)          │ (Port 3306)
    ▼ (Private Data Subnet) ▼ (Private Data Subnet)
[ RDS MySQL Database ]  [ AWS Secrets Manager ]
