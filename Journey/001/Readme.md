[<img alt="alt_text" width="800px" height="400px" src="https://images.unsplash.com/photo-1611108163374-a1cc7722f093?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=869&q=80" />]()

# Launch a website on AWS EC2

## Introduction

I chose this project to learn and document how to setup a basic website on an AWS EC2 instance.

## Prerequisite

The base knowledge required is setting up an AWS account, launching an EC2 instance and basic linux command line experience.

## Use Case

### Basic Diagram
[<img alt="alt_text" width="650px" height="500px" src="https://s3.us-west-2.amazonaws.com/santiamdigital.com/100DaysOfCloud/AWS-EC2-Diagram.png" />]()
</br>
This is a useful skill to setup a basic website and gain experience with linux, security groups and AWS. 

## Cloud Research

- The first main decision is to figure out which cloud provider you want to experiment with. The top tier cloud providers are AWS (Amazon), Azure (Microsoft) and GCP (Google). There are tier 2 providers but I'd recommend checking out Tier 3 providers like Vultr or Linode if you're looking for alternatives to the top tier providers.
- When just starting out with AWS, utilize the free tier eligible servers for learning. The most popular Linux distributions appear to be Ubuntu for personal learning, CentOS if you're looking for something comparable to Red Hat (Enterprise version). The main differences you'll notice as a beginner are installing programs. For Ubuntu, you'll use 'apt' and for CentOS you'll use 'rpm' to manage packages and install programs.

## Try yourself

In this mini-tutorial, we'll go through setting up an AWS EC2 instance, install an application to host a website, and create an HTML file to display information on the website.

### Step 1 — Launch a linux based EC2 instance.
- After logging in to the AWS console (https://console.aws.amazon.com/), search for the EC2 (Elastic Compute Cloud) and then click on 'Launch Instances'.
- In the launch wizard you'll need to select the AMI (Amazon Machine Image) to use for your server. Search for 'ubuntu' and select the newest version that also says 'free tier eligible'. The launch wizard will also allow you to create and download a keypair (.pem file) to your local machine. The .pem file will be required to establish a remote SSH connection to your server.

![Screenshot](https://s3.us-west-2.amazonaws.com/santiamdigital.com/100DaysOfCloud/AWS-EC2-Choose-AMI.png)

### Step 2 — Setup security group that allows http/https connections from the internet and ssh connections.
- In order to connect to the remote linux server, you'll need to open port 22 to establish the SSH connection. Ports are like gates that can be opened or closed to allow a connection through to the server. Allowing connections through on port 443 (HTTPS) and 80 (HTTP) will make it possible for your website to load up in a web browser. If you select the source 'my ip' that will restrict connections to your IP address only. If you select 'anywhere' the website will be available to anyone but also open your linux server to connections from anywhere as well (proceed with caution).

![Screenshot](https://s3.us-west-2.amazonaws.com/santiamdigital.com/100DaysOfCloud/AWS+Security+Rules-My-IP.png)

### Step 3 — Connect to Remote Server
Navigate to the EC2 instance in AWS. Select the Instance ID link to display an information summary. Select 'Connect' and then 'SSH client' for instructions on how to connect to the server. Copy the SSH connection link 'ssh -i "linux-webserver-ed25519.pem" ubuntu@ec2-35-88-202-8.us-west-2.compute.amazonaws.com'.
From your local machine's command line, navigate to the folder where your .pem file (AWS Keypair) is located and then paste the copied SSH connection command to the console and press enter.

![Screenshot](https://s3.us-west-2.amazonaws.com/santiamdigital.com/100DaysOfCloud/SSH+Connection.png)

### Step 4 — Install webserver application on the EC2 instance.
After you connect to the remote server, update the package repository and then install the webserver application.
From the command line, type in 'sudo apt update -y' and then 'sudo apt install nginx -y'. The first command updates the package list so you'll install the newest version of the webserver application (nginx).
After installing the nginx webserver, type in 'sudo systemctl status nginx' to verify the application is running.
Then, navigate to the public IP address of the AWS EC2 instance (check Instance Summary Information) in your web browser. If nginx is running then you will see a 'Welcome to nginx!' web page.

![Screenshot](https://s3.us-west-2.amazonaws.com/santiamdigital.com/100DaysOfCloud/Welcome-to-nginx.png)

### Step 5 — Create index.html file for the webserver to display HTML on the website.
By default, the 'Welcome to nginx!' html file will be located in the /var/www/html directory.
Navigate to the /var/www/html directory (hint: use cd command) and create a file named 'index.html' (see touch, nano, or vim commands).
Edit the newly created index.html file and add your message 'Hello and welcome to my website!'.
Save the file and exit.

![Screenshot](https://s3.us-west-2.amazonaws.com/santiamdigital.com/100DaysOfCloud/Create-Index-html.png)

### Step 6 — Enter the public IP address in a web browser to verify the website is up and running.
In your web browser, refresh the 'Welcome to nginx!' webpage or re-enter the public IP address and you should now see the updated index.html file displaying in your web browser.

![Screenshot](https://s3.us-west-2.amazonaws.com/santiamdigital.com/100DaysOfCloud/Hello.png)

## ☁️ Cloud Outcome

This was a great day 1 exercise for #100DaysOfCloud. I didn't realize all the mini-steps needed to setup a basic website but this experience teaches you how to get started in AWS, use basic linux commands and get familiar with networking and security.

## Next Steps

Next, I'd like to explore AWS further and find a small project that will help prepare me for the Certified Cloud Practicioner Exam.
## Social Proof

![Screenshot](https://s3.us-west-2.amazonaws.com/santiamdigital.com/100DaysOfCloud/LinkedIn-day-1.png)

[Twitter](https://twitter.com/Alex_Santiam)
[LinkedIn](https://www.linkedin.com/in/alex-romero-i2049/)
