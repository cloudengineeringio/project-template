# Cloud Engineering Infrastructure Project

A comprehensive AWS infrastructure project demonstrating modern cloud engineering practices with Terraform, Auto Scaling Groups, Application Load Balancers, and monitoring.

## Details

| Property | Value |
|---|---|
| **Difficulty** | Intermediate |
| **Provider** | AWS |
| **Estimate** | 2-4 hours |
| **Labels** | Infrastructure, Compute, Networking, Monitoring |

## Tech Stack

- **AWS VPC** - Virtual Private Cloud with public/private subnets
- **Application Load Balancer** - High availability traffic distribution
- **Auto Scaling Group** - Automatic scaling based on demand
- **EC2 Instances** - Web servers with Apache and PHP
- **S3 Bucket** - Log storage and backup
- **CloudWatch** - Monitoring and logging
- **Terraform** - Infrastructure as Code

## Prerequisites

- AWS CLI configured with appropriate credentials
- Terraform >= 1.0 installed
- Basic understanding of AWS services
- Git for version control
- Terminal/Command line access

## Project Overview

This project creates a production-ready, highly available web application infrastructure on AWS. It demonstrates modern cloud engineering practices including Infrastructure as Code, auto-scaling, load balancing, and comprehensive monitoring.

**What You'll Build**: A scalable web application infrastructure with:
- Multi-AZ deployment for high availability
- Auto-scaling web servers behind a load balancer
- Private networking for security
- Centralized logging and monitoring
- Automated deployment scripts

**Key Features:**
- ✅ **High Availability** - Multi-AZ deployment with Auto Scaling
- ✅ **Security** - Private subnets and security groups
- ✅ **Monitoring** - CloudWatch logs and custom monitoring
- ✅ **Scalability** - Auto Scaling Group with load balancer
- ✅ **Cost Optimization** - Configurable instance types and scaling

> **Note**: This infrastructure will create AWS resources that may incur costs. Always review the configuration and clean up resources when done.

**Sample Deployment Command:**
```bash
cd terraform
terraform init
terraform plan
terraform apply
```

**Configuration Example:**
```hcl
# terraform.tfvars
aws_region = "us-west-2"
project_name = "my-web-app"
environment = "production"
instance_type = "t3.small"
min_size = 2
max_size = 10
desired_capacity = 3
```

## Key Components

| Component | Purpose | Technology |
|---|---|---|
| VPC | Network isolation and security | AWS VPC |
| Application Load Balancer | Traffic distribution and health checks | AWS ALB |
| Auto Scaling Group | Automatic scaling based on demand | AWS ASG |
| EC2 Instances | Web application servers | AWS EC2 |
| S3 Bucket | Log storage and backup | AWS S3 |
| CloudWatch | Monitoring and alerting | AWS CloudWatch |

## Architecture

This project implements a three-tier architecture with the following components:

![Architecture](images/diagram.png "Architecture diagram")

The architecture includes:
- **Public Subnets**: Host the Application Load Balancer
- **Private Subnets**: Host the web application servers
- **Auto Scaling Group**: Manages EC2 instances across multiple AZs
- **S3 Bucket**: Stores application logs and backups
- **CloudWatch**: Monitors application and infrastructure metrics

**Design Principles:**
- **Security First**: Private subnets for application servers
- **High Availability**: Multi-AZ deployment
- **Scalability**: Auto-scaling based on demand
- **Monitoring**: Comprehensive logging and metrics

## Learning Objectives

- **Infrastructure as Code**: Learn Terraform best practices
- **AWS Networking**: Understand VPC, subnets, and security groups
- **Auto Scaling**: Implement dynamic scaling based on demand
- **Load Balancing**: Distribute traffic across multiple instances
- **Monitoring**: Set up CloudWatch logs and custom monitoring

## Tasks

## Phase 1: Infrastructure Setup

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-01** | Initialize Terraform and configure AWS provider | ⬜ |
| **TASK-02** | Create VPC with public and private subnets | ⬜ |
| **TASK-03** | Set up Internet Gateway and route tables | ⬜ |

## Phase 2: Security Configuration

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-04** | Create security groups for web servers | ⬜ |
| **TASK-05** | Configure Application Load Balancer security | ⬜ |
| **TASK-06** | Set up S3 bucket with encryption and versioning | ⬜ |

## Phase 3: Application Deployment

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-07** | Create launch template with user data script | ⬜ |
| **TASK-08** | Configure Auto Scaling Group with health checks | ⬜ |
| **TASK-09** | Set up Application Load Balancer and target groups | ⬜ |

## Phase 4: Monitoring and Logging

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-10** | Configure CloudWatch log groups | ⬜ |
| **TASK-11** | Set up custom monitoring scripts | ⬜ |
| **TASK-12** | Test application health endpoints | ⬜ |

## Phase 5: Testing and Validation

| Task ID | Description | Status |
|---|---|:---:|
| **TASK-13** | Deploy infrastructure and verify components | ⬜ |
| **TASK-14** | Test load balancer and auto-scaling functionality | ⬜ |
| **TASK-15** | Run monitoring scripts and validate logs | ⬜ |

## Success Criteria

- Infrastructure deploys successfully without errors
- Application is accessible via load balancer DNS
- Auto Scaling Group scales instances correctly
- CloudWatch logs are being generated
- Security groups restrict access appropriately
- S3 bucket stores logs with encryption enabled

## Bonus Challenges

- **SSL/TLS**: Add SSL certificate and HTTPS support
- **Database**: Integrate RDS database with the application
- **CI/CD**: Set up automated deployment pipeline
- **Advanced Monitoring**: Add custom CloudWatch metrics and alarms
- **Multi-Region**: Deploy infrastructure across multiple regions

## Quick Start

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd project-template
   ```

2. **Configure AWS credentials:**
   ```bash
   aws configure
   ```

3. **Deploy infrastructure:**
   ```bash
   ./scripts/deploy.sh
   ```

4. **Monitor the deployment:**
   ```bash
   ./scripts/monitor.sh
   ```

5. **Access your application:**
   ```bash
   # Get the load balancer DNS
   terraform output load_balancer_dns
   ```

## Project Structure

```
project-template/
├── terraform/
│   ├── main.tf              # Main infrastructure resources
│   ├── variables.tf         # Input variables
│   ├── outputs.tf          # Output values
│   ├── user_data.sh        # EC2 bootstrap script
│   └── README.md           # Terraform-specific documentation
├── scripts/
│   ├── deploy.sh           # Deployment automation script
│   └── monitor.sh          # Monitoring and health check script
├── images/
│   └── diagram.png         # Architecture diagram
└── README.md               # This file
```

## Resources

- [Terraform AWS Provider Documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [AWS VPC User Guide](https://docs.aws.amazon.com/vpc/)
- [Application Load Balancer Guide](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/)
- [Auto Scaling User Guide](https://docs.aws.amazon.com/autoscaling/)
- [CloudWatch Logs Documentation](https://docs.aws.amazon.com/cloudwatch/logs/)
- [AWS S3 User Guide](https://docs.aws.amazon.com/s3/)

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

If you encounter any issues or have questions:
- Open an issue on GitHub
- Check the troubleshooting section in the Terraform README
- Review AWS documentation for specific service issues