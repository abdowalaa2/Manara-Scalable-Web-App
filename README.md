# Scalable Web Application with ALB and Auto Scaling

![Architecture Diagram](manara.drawio.svg)

## Architecture: EC2-based

Deploy a simple web application on AWS using EC2 instances, ensuring high availability and scalability with Elastic Load Balancing (ALB) and Auto Scaling Groups (ASG). The project demonstrates best practices for compute scalability, security, and cost optimization.

This architecture automatically handles traffic spikes by adding more servers when needed and removes them when traffic is low, helping you save money while keeping your application running smoothly.

## Project Overview

This project creates a production-ready web application infrastructure on AWS that can handle thousands of users simultaneously. The system automatically adjusts to traffic changes, ensuring your application performs well during both quiet periods and traffic spikes.

The architecture follows AWS best practices for security, reliability, and cost optimization. All components work together to create a fault-tolerant system that can recover from failures automatically.

## How It Works

1. **Traffic comes in** through the Application Load Balancer
2. **Load Balancer distributes** requests across healthy EC2 instances
3. **Auto Scaling monitors** CPU usage and request counts
4. **New instances launch** automatically when traffic increases
5. **Instances terminate** automatically when traffic decreases
6. **Database stores** application data with automatic backups

## Key AWS Services Used

### EC2
Launch instances for the web app. These virtual servers run your application code and can be automatically created or removed based on demand.

### Application Load Balancer (ALB)
Distributes traffic across multiple instances. Acts as a smart traffic director that only sends requests to healthy servers and can handle SSL certificates.

### Auto Scaling Group (ASG)
Ensures instances scale based on demand. Automatically adds servers when busy and removes them when quiet, keeping your app available 24/7.

### Amazon RDS (Optional)
Backend database (MySQL/PostgreSQL) with Multi-AZ. Managed database service that handles backups, updates, and failover automatically.

### IAM
Role-based access to instances. Security service that controls what each server can access without storing passwords on the servers.

### CloudWatch & SNS
Monitor performance and send alerts. CloudWatch watches your system metrics, and SNS sends you notifications when something needs attention.

## Benefits

- **High Availability**: Your app stays online even if servers fail
- **Cost Effective**: Only pay for servers you actually need
- **Automatic Scaling**: No manual intervention needed during traffic spikes  
- **Secure**: Built-in security features and isolated network
- **Managed Database**: No database maintenance headaches

## Learning Outcomes

### Setting up secure and scalable EC2-based web applications
Learn how to configure EC2 instances with proper security measures and deploy web applications that can handle varying traffic loads. You'll understand server configuration, security groups, and application deployment.

### Implementing high availability using ALB and ASG
Understand how to set up load balancers and auto scaling to ensure your application stays available even when individual instances fail. Master traffic distribution and automatic failover.

### Optimizing costs and performance using Auto Scaling policies
Learn to create scaling rules that automatically add or remove instances based on demand, keeping costs low while maintaining good performance. Understand when to scale up and down based on real metrics.

## Architecture Components

### Network Setup
- **VPC (Virtual Private Cloud)**: Creates an isolated network environment
- **Public Subnets**: Host the load balancer for internet access
- **Private Subnets**: Host application servers for enhanced security
- **Multiple Availability Zones**: Spread resources across different data centers

### Security Features
- **Security Groups**: Control network traffic like virtual firewalls
- **IAM Roles**: Provide secure access without storing passwords
- **Network Isolation**: Keep database and application servers private
- **SSL/TLS Support**: Encrypt data in transit

## Scaling Behavior

### When Traffic Increases
1. CloudWatch detects high CPU usage (above 70%)
2. Auto Scaling Group launches new EC2 instances
3. New instances automatically register with the load balancer
4. Traffic gets distributed across all healthy instances
5. System handles increased load seamlessly

### When Traffic Decreases
1. CloudWatch detects low CPU usage (below 30%)
2. Auto Scaling Group terminates excess instances
3. Remaining instances handle the reduced load
4. You only pay for what you need

### Scaling Limits
- **Minimum Instances**: 2 (always running for availability)
- **Maximum Instances**: 10 (prevents runaway costs)
- **Scaling Speed**: New instances launch in 2-3 minutes

## Database Configuration

### RDS Features
- **Multi-AZ Deployment**: Database runs in multiple data centers
- **Automatic Backups**: Daily backups kept for 7 days
- **Read Replicas**: Additional database copies for better performance
- **Automatic Updates**: Security patches applied automatically
- **Monitoring**: Performance insights and slow query detection

### Database Security
- **Private Subnets**: Database not accessible from internet
- **Encryption**: Data encrypted both at rest and in transit
- **Access Control**: Only application servers can connect
- **Regular Snapshots**: Point-in-time recovery available

## Monitoring and Alerts

### CloudWatch Metrics
- **CPU Utilization**: Track server performance
- **Memory Usage**: Monitor application memory consumption
- **Network Traffic**: Measure data transfer
- **Request Count**: Monitor application load
- **Response Time**: Track application performance
- **Error Rates**: Detect application issues

### Alert Notifications
- **Email Alerts**: Get notified of critical issues
- **Scaling Events**: Know when instances are added/removed
- **Health Check Failures**: Immediate notification of problems
- **Database Issues**: Alerts for database performance problems
- **Cost Alerts**: Warnings when spending exceeds thresholds

## Cost Optimization

### Automatic Cost Control
- **Right-sizing**: Use appropriate instance types for workload
- **Scheduled Scaling**: Scale down during off-hours
- **Spot Instances**: Use cheaper instances for development
- **Reserved Instances**: Commit to instances for bigger discounts

### Cost Monitoring
- **Resource Tagging**: Track costs by project and environment
- **Monthly Reports**: Understand spending patterns
- **Budget Alerts**: Get warned before exceeding budgets
- **Usage Analytics**: Identify optimization opportunities

## Deployment Process

### Prerequisites
- AWS Account with administrative access
- Basic understanding of web applications
- Familiarity with AWS Console
- Knowledge of networking concepts

### Step-by-Step Setup
1. **Create VPC and Subnets**: Set up isolated network environment
2. **Configure Security Groups**: Define traffic rules for each component
3. **Set up IAM Roles**: Create secure access permissions
4. **Deploy RDS Database**: Launch managed database service
5. **Create Launch Template**: Define server configuration
6. **Configure Auto Scaling**: Set up automatic scaling rules
7. **Deploy Load Balancer**: Create traffic distribution system
8. **Test Application**: Verify all components work together

### Testing the System
- **Load Testing**: Simulate high traffic to test scaling
- **Failure Testing**: Remove instances to test failover
- **Performance Testing**: Measure response times under load
- **Security Testing**: Verify access controls work properly

## Common Use Cases

### E-commerce Websites
Handle shopping traffic spikes during sales events while maintaining fast page loads and secure transactions.

### Content Management Systems
Serve articles and media to large audiences with automatic scaling during viral content moments.

### API Services
Provide reliable backend services for mobile apps and third-party integrations with consistent performance.

### Business Applications
Run internal company applications with high availability and security for remote teams.

## Troubleshooting Guide

### Instance Launch Issues
- Check security group configurations
- Verify IAM role permissions
- Review subnet and availability zone settings
- Confirm instance limits not exceeded

### Database Connection Problems
- Verify security group allows database traffic
- Check database credentials and endpoint
- Ensure instances are in correct subnets
- Review network ACL settings

### Load Balancer Health Check Failures
- Confirm application responds on correct port
- Check health check path configuration
- Verify security groups allow health check traffic
- Review application logs for errors

### Scaling Issues
- Monitor CloudWatch metrics and alarms
- Check Auto Scaling Group settings
- Verify scaling policies are correctly configured
- Review instance launch errors in Auto Scaling logs
