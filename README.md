# Deploy a High-Availability Web Application Using AWS CloudFormation - IaaS 


Infrastructure-as-code (IAC) that automates the process of creating a secured and high-availability environment and deploying an application (packaged and staged in AWS S3 Storage) Apache Web Server. The script contains all the configurations needed for a repeatable process so that the infrastructure can be discarded and recreated at will multiple times.

**Features**

1. Load-balanced servers with auto-scaling capability across two availability zones within a single region.

2. Server/instance specification: 2vCPUs, 4GB RAM, 10GB disk space.

3. Linux Operating System using the Ubuntu distribution machine image.

4. Compute instances are secured in a private subnet.

5. Load-balancer, and application servers have security groups defined with only needed ports opened.

6. Application servers have outbound internet access via NAT gateway for critical OS updates and patches.

7. Sample application code is packaged and stored in an S3 bucket with IAM permissions.

8. Application servers are configured with IAM instance profile to be able to access and download application code from AWS S3 bucket.

9. Application code is deployed in a apache web server for added security and isolation.

10. Health checks and thresholds are defined to aid in system availability detection. Metrics are collected, aggregated, and monitored via AWS CloudWatch.

11. Entire environment is fully virtualized in a cloud platform that can be taken down and brought back up within a short period of time. The process of creating and starting all the services, spinning up instances are automated via scripts in this repo.

**Detailed Infrastructure Architecture**
![GitHub Logo](https://github.com/iNomanIkram/IaaS-HighlyAvailableWebApp-CloudFormation/blob/master/Diagram/Project.png)

**Prerequisites**
1. Make sure you have all setup an AWS account.
2. AWS cli is install and configured.
3. Create an S3 storage in your AWS account and upload the sample code udacity.zip. Besure to change the name of **bucket** in s3 url of **UserData** in servers.yml file.

**Steps**
1. Clone the git repository.
2. There are two components to standing up our environment in AWS: infra and servers. Infrastructure are the VPCs, gateways, subnets, and routing. Servers are the compute resources, load-balancers, and auto-scaling.

Infrastructure must be setup first. Run the command below with an arbitrary stack name e.g. 'infra' from Network Infrasturcture Folder.
```
./infra-create.sh <stack name> infra.yml infra-parms.json
```

Once infrastructure has been completed (by checking AWS CloudFormation for stack status), run the command below and assigning another arbitrary stack name e.g. 'servers' from Servers Folder.

```
./servers-create.sh <stack name> servers.yml servers-params.json
```

3. Check status of the stacks. Once complete and to test the environment is setup, navigate to EC2 Dashboard - Load Balancers and copy the DNS name to your browser.

