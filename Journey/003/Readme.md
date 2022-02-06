# Day 3 - Elastic Load Balancer

# EC2: Elastic Load Balancer

## Introduction

This topic is the next step in studying for the AWS CCP Exam. Elastic Load Balancing (ELB) will help to automatically distribute traffic across different servers to help reduce your application from being overloaded. In AWS, you can setup a Load Balancer to distribute traffic across different availability zones. This will also help with redundancy in the event that an Availability Zone (AZ) goes down then your application will still be reachable via another AZ.

## Prerequisite

Recommended learning would include setting up a basic EC2 instance.

## Use Case

Your application is being overloaded with traffic and users are reporting issues with performance, freezing or crashing. Implement an Elastic Load Balancer to distribute the traffic between multiple resources.

## Cloud Research

In AWS, there are 3 main load balancer types (Application, Network and Gateway).

### Type 1: Application Load Balancer

The Application Load Balancer is useful when you need flexibility to manage HTTP and HTTPS traffic. 

This type operates at the request level and provides advanced routing and visibility features targeted at application architectures (includes microservices such as AWS Lambda and containers).

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff80b18d0-de5b-45e1-8894-389a3627b372%2FUntitled.png?table=block&id=f4c0afdf-e629-4922-a825-bf71250bede6&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=880&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

### Type 2: Network Load Balancer

The main uses for a Network Load balancer are when you need TLS offloading at scale, centralized certificate deployment, support for UDP, and static IP Addresses for your applications.

This type operates at the connection level and is capable of handling millions of requests per second securely and quickly.

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5e2357c1-0276-4338-8101-bb3bf3fb2b0a%2FUntitled.png?table=block&id=98c46f2d-0851-483c-8be8-f0a04649f0b7&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=870&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

### Type 3: Gateway Load Balancer

Gateway Load Balancers enable you to deploy, scale, and manage virtual appliances, such as firewalls, intrusion detection and prevention systems, and deep packet inspection systems. It combines a transparent network gateway (that is, a single entry and exit point for all traffic) and distributes traffic while scaling your virtual appliances with the demand.

![SCreenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fbda0a937-e1e0-4eb1-9195-737a707ad07a%2FUntitled.png?table=block&id=3b077525-b563-4246-bf32-8068e398683c&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=920&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

## Try yourself

### Step 1 — Create two EC2 instances

From EC2, launch 2 instances that we’ll use to test out our load balancer. For this tutorial, we’ll use the AMI that we recently created to launch two new Ubuntu instances.

After the instances are initialized, update the ‘Name’ field to ‘Webserver A’ and ‘Webserver B’ to help identify the two servers we want the load balancer to distribute traffic across.

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7cc766fd-dc08-46eb-ae80-673904f6417a%2FUntitled.png?table=block&id=2285fc5c-09a2-4614-85f3-da784c957210&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1280&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

### Step 2 — Create a Load Balancer

From EC2, under Load Balancing, select Load Balancers.

Select ‘Create Load Balancer’.

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F07951597-737c-4195-ac3c-2e1c10c39ad9%2FUntitled.png?table=block&id=fdc0a930-f13b-43d5-898b-03df3c66c2cd&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1280&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

Select the ‘Application Load Balancer’ type and click ‘Create’.

Enter the Basic Configuration information: 

- Load balancer name (AppLoadBalancer)
- Scheme (Internet-facing)
- IP address type (IPv4)

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3bcd8bed-7b4c-4779-8543-25b2f2946b5d%2FUntitled.png?table=block&id=6f97d50f-4594-4ab0-b24e-05d39c5fe092&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1280&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

Enter the Network Mapping information:

- Use the default VPC (Virtual Private Cloud) selected.
- For Mappings, select two Availability Zones
    - Make sure that the instances you created are in the same Availability Zones you’re selecting otherwise the Load Balancer will be unable to forward traffic.

Under Security groups, use the default security group.

Listeners and routing, keep the default listener HTTP:80 and select ‘Create target group’.

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd4a89998-dc8d-459b-aba9-97e9a1741e98%2FUntitled.png?table=block&id=f97857f8-9082-452f-8304-2c739206150c&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1280&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

### Step 3 — Create target group

For a Basic Configuration, set the following parameters:

Choose a target type: Instances

*Other options would include: IP addresses, Lambda functions and Application Load balancers.

Enter a Target group name: Target-Group

Use the defaults for Protocol Version and Health checks.

Click ‘Next’.

### Step 4 — Register Targets

From the available instances, select the two instances that were created in step 1 (Webserver A and Webserver B) to add to our target group.

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fcb3839fe-24dd-401b-889e-ed0c5d291426%2FUntitled.png?table=block&id=bec81349-c00d-46fb-a65d-232650ad91b0&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1280&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

Select ‘Include as pending below’.

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9e5a943a-b72c-4423-adb2-c0e571b5bc6e%2FUntitled.png?table=block&id=c9f302d4-124d-4a41-b94b-3bbbe203960c&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1280&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

Review the selected Targets and click ‘Create target group’.

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7a094e05-7a36-4540-b2a6-43bb864972e8%2FUntitled.png?table=block&id=00662988-11f8-4f0d-a45b-de8b3187cb10&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1280&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

### Step 5 - Create Load Balancer

Navigate back to the load balancer creation wizard.

From the Listeners and routing section, you should now be able to select the newly created Target Group.

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd5dd0f02-94e1-4cdc-8891-3512f08170ea%2FUntitled.png?table=block&id=9327a408-2a12-43e2-b61b-5d06fdf68492&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1280&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

Review the configuration summary and select ‘Create load balancer’.

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F4a28788b-55fb-459a-91a9-55e473fcb80e%2FUntitled.png?table=block&id=1044dae4-1dca-45a2-a169-6156e6abb29b&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1280&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

After the load balancer finishes provisioning, the DNS name for the load balancer will be functional.

The new traffic flow would start with the load balancer’s DNS name, then route to the Listener (HTTP: 80) which would then check the target group rules and forward traffic accordingly to the original EC2 instances that were created.

## ☁️ Cloud Outcome

With this project, I learned about the different types of load balancers (Application, Network, Gateway) and gained experience setting up an Application Load Balancer. I learned that the instances, target group, and load balancer need to be mapped to the same availability zones otherwise there will be no destination for the traffic to route to.

## Next Steps

For next steps, I’ll learn about the Amazon S3 (Simple Storage Service) product.
