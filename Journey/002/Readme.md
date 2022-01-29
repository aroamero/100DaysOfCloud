# Day 2 - AMI and AutoScaling Groups

# EC2: AMI (Amazon Machine Image) and AutoScaling Groups

## Introduction

The next few topics (AMI and AutoScaling Groups) are still within EC2. These areas will help with creating a base image to use in AutoScaling Groups.

## Prerequisite

Recommended learning would include setting up a basic EC2 instance.

## Use Case

Your website is being overloaded with traffic and you need to scale up resources to handle the increased demand on your EC2 instance. How can you create scalability for your website?

## Try yourself

### Step 1 — Create an AMI (Amazon Machine Image)

In order to create an AMI, first, you’ll need to launch an EC2 instance with your desired operating system. 

For this tutorial, we’ll setup an Ubuntu 20.04 instance. 

After the instance is created, then navigate to the EC2 Dashboard and select ‘Instances’.

Select the Instance to create an image of.

Then, select Actions > Images and templates > Create image

![Screenshot](https://destiny-jump-4a2.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fd5b7ec90-4789-469f-8ea1-b6a356de0a8d%2FUntitled.png?table=block&id=8c252bda-c4e4-4ec4-b5c1-5d6710585b8b&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=2000&userId=&cache=v2)

Once the image builder loads up, enter a name for your image and an optional description.

Lastly, select ‘Create image’

### Step 2 — Create a Launch Configuration

Before creating an AutoScaling Group, a Launch Configuration is needed. Navigate to the EC2 Dashboard and select ‘Launch Configurations’ under ‘Auto Scaling’.

Select ‘Create launch configuration’. 

![Screenshot](https://destiny-jump-4a2.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fac088c18-a243-4d53-9e22-901bec76757f%2FUntitled.png?table=block&id=1815365c-a3c3-4f04-94c9-599ad93865a3&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=2000&userId=&cache=v2)

Add a launch configuration name, select the AMI, choose an Instance Type (t2.micro).

Additional configuration options include: Purchasing Option, IAM instance profile, Monitoring, and EBS-Optimized instance.

From this page, you can also add additional Storage Volumes, select Security Groups, and designate a Key Pair to connect to the instances.

![Screenshot](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fe46be038-c4f1-40ef-88db-ed4725b5a811%2FUntitled.png?table=block&id=88aac5c8-4c43-48e0-99b1-a4c38b875687&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1280&userId=a6f0a3b0-65db-4305-8c72-b90bdb1d5173&cache=v2)

Select ‘Create Launch Configuration’.

![Screenshot](https://destiny-jump-4a2.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F67e83ea9-8e4b-495f-85c1-2b9f4e08d574%2FUntitled.png?table=block&id=121c8282-5f49-45e7-ba01-435bd86c5996&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=2000&userId=&cache=v2)

### Step 3 — Create Launch Template

Now that the launch configuration has been created. You can create a Launch Template.

From Launch Configurations, select the specific launch configuration you just created. 

Select ‘Copy Selected’ from the ‘Copy to Launch Template’ drop down box.

![Screenshot](https://destiny-jump-4a2.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F15b56566-dca9-4891-84f5-0c1ecc9a9787%2FUntitled.png?table=block&id=6b09b48f-9469-4c58-87b9-1cc76fe7d639&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=2000&userId=&cache=v2)

Edit the  ‘New launch template name’ so there are no spaces in the name.

Add a ‘check’ to ‘Create an Auto Scaling group using the new template.

Select ‘Copy’.

![Screenshot](https://destiny-jump-4a2.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Faffc1ee3-93cd-477d-b8d4-5d9d41d3f8ae%2FUntitled.png?table=block&id=62c7ac40-024f-4c77-aad9-83df9bd2527e&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1780&userId=&cache=v2)

### Step 4 - Create and Auto Scaling Group

The Auto Scaling Group creation wizard should display. If not, proceed with the following steps.

From the EC2, select Auto Scaling > Auto Scaling Groups.

Select ‘Create Auto Scaling group’

Enter a name for the Auto Scaling Group, select the Launch Template, and then click ‘Next’.

![Screenshot](https://destiny-jump-4a2.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc5a6e240-5e92-484a-9a89-f3c1d3f7762d%2FUntitled.png?table=block&id=8f41bb5b-b553-4598-9421-f642157831db&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=1850&userId=&cache=v2)

![Screenshot](https://destiny-jump-4a2.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fbe3e24f9-c175-4d64-b12b-3fd3c47c8bb3%2FUntitled.png?table=block&id=09c873fa-d0b1-483b-a94c-f4a51c2e69ed&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=2000&userId=&cache=v2)

![Screenshot](https://destiny-jump-4a2.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F2655d80d-0da9-402f-a461-f1363b1bf790%2FUntitled.png?table=block&id=33d5918f-987e-4348-8f51-a7c69299a532&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=2000&userId=&cache=v2)

From Network, Select a few Availability Zones to create additional redundancy.

![Screenshot](https://destiny-jump-4a2.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa0b7c96f-b617-477d-8819-62871d5819b5%2FUntitled.png?table=block&id=cf3355f4-5465-4246-b2fa-d222eb9a5500&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=2000&userId=&cache=v2)

Review the Instance type requirements and select ‘Next’.

![Screenshot](https://destiny-jump-4a2.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F40e8384c-0384-4c9f-9f36-4a1f19c792d3%2FUntitled.png?table=block&id=eef30aae-1ebd-4037-866c-785f3af23296&spaceId=33b16dcc-d006-4ad9-8f62-15abd9fafc7f&width=2000&userId=&cache=v2)

Optional Advanced Options include:

- Load Balancing (Application and Network)
- Health Checks (EC2 and ELB) automatically replace instances that fail health checks.
- Monitoring (CloudWatch) to collect group metrics.

Configure group size and scaling policies. The default desired, minimum and maximum capacity is set to ‘1’.

Optional scaling policies include:

- Target tracking scaling policy based on the following metrics:
    - Average CPU utilization, network in/out and Application Load Balancer request count per target.
- Instance scale-in protection to prevent newly launched instances from scale in by default.

Select ‘Next’.

Optionally Add notifications (SNS topics) to capture when instances are launched or terminated in the Auto Scaling group.

Select ‘Next’.

Optionally at a Tag and select ‘Next’.

Review the Auto Scaling Group configuration and select ‘Create Auto Scaling group’.

Instances will now automatically scale up or down based on the AMI you created and the autoscaling options selected.

To test out the group, navigate to EC2 Instances and terminate one of the new instances.

The Auto Scaling Group should automatically replace the terminated instance with a new instance.

## ☁️ Cloud Outcome

With this project, I learned how to create a basic template to use in an auto scaling group. I went from creating a standalone instance to a group that will automatically adjust and correct itself based on the requirements of the project.

## Next Steps

For next steps, I’m interested in learning about Elastic Load Balancers in AWS.
