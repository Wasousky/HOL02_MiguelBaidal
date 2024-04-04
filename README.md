
HOL 02: Deploying a hybrid infrastructure for researchers in AWS
======


##### HIGH-PERFORMANCE AND DISTRIBUTED COMPUTING FOR BIG DATA


#### **Miguel Baidal Marco**

---

$~~~~~~~~~~~$

#### 1. Public key HOL02.

After completing the setup, I imported the public key to AWS EC2, naming it HOL02. This ensures that I can securely access my instances using SSH authentication and all the instances can be created correctly.

![Key pairs mapping](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6b58aea1-bb19-4ded-a87e-f866b72d7508)

$~~~~~~~~~~~$

#### 2. VPC, subnets, route tables, security groups, and EC2 instances configuration

Fistly, I've created a VPC called HOL02-VPC with the address range 10.0.0.0/16.

![HOL02-VPC creation](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/11972151-05df-4456-b4ed-dc5f8f4b6812)

In this VPC, I've established three subnets referred to as HOL02-DMZ, HOL02-Production, and HOL02-Research, each configured with the required IP ranges as specified in the exercise.

However, I've only included a screenshot illustrating the creation process of one of the three subnets.

![HOL02-DMZ creation steps](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/7b6986a6-6662-4d48-84bb-ddf3472e918c)

![The three subnets listed](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/d6b813f5-ba5d-4143-9f6d-9c6798f104f8)

Following that, I set up an Internet Gateway called HOL02-IGW and linked it to the HOL02-VPC, enabling connectivity to the internet.

![Internet Gateway creation](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/5b08dcc6-4782-4e19-962a-cee4e387917b)

![VPC - Internet Gateway linking](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/b95bbd3b-0ac1-4f9d-8939-4cf5bbe074be)

Then, I've established three route tables: HOL02-DMZ-RT, HOL02-Production-RT, and HOL02-Research-RT.

![HOL02-DMZ-RT creation](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/a7c3fdda-256c-4452-936d-e7fdc0b9bf5b)

![The three route tables listed](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/363fe5db-3760-452b-906b-3e8cb615fcc4)

Each route table is associated with its respective subnet.

![Route table and subnets association](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/fc553448-551d-40a2-ae68-2f88e00c1cf5)

Later, I've configured three security groups:
- HOL02-DMZ-SG, that allows traffic on ports 22, 443, 943, 945, and 1194.

![HOL02-DMZ-SG](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6792af10-bf8f-446e-9cf0-60864309ee90)


- HOL02-Production-SG, that permits traffic on ports 80, 443, and 22 only from HOL02-DMZ-SG



- HOL02-Research-SG, that allows traffic on ports 22 and 8888 only from HOL02-DMZ-SG.

![Port 8888 allows traffic only from HOL02-DMZ-SG](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/a315710d-ff07-486b-bf94-9c677c3e06a4)


Moreover, I've launched three EC2 instances:
![Instances listed](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6850f58d-eb76-4459-bcda-c31b49928eef)

- HOL02-VPN is placed in HOL02-DMZ subnet using Ubuntu 22.04 LTS AMI, and it has been associated with an Elastic IP.

![HOL02-VPN instance](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/ceb615f8-e7ef-45ac-8262-91d1e9fc55d6)

![Elastic IP association](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/10d00352-983e-4680-96fc-0f67cfcf2ffe)


- HOL02-VoilaServer is in HOL02-Production subnet using Amazon Linux 2 AMI.

- HOL02-Jupyter is in HOL02-Research subnet also using Amazon Linux 2 AMI.

Finally, I've created an S3 bucket named HOL02-notebooks-baidal. All the files used are uploaded to this bucket.

![Bucket creation](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6823cdad-4d1a-480f-96b5-34b073dfb76b)

![Files uploaded to the S3 bucket](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/443a353a-e970-4faa-ae75-c66bfdba3ffc)

Moreover, to get everything correctly set, it is needed to edit the different rouying tables and apply an Internet Gateway to allow the Internet traffic.

![Internet Gateway creation](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6fa6e475-35f8-4014-ab7d-964697299e32)

As it can be seen in the Resources Map, the VPC, the subnets, the route tables and the Internet Connection are all well created and linked.

![Resources map](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/8636833a-8790-4665-9a51-6a0f3e77a497)

$~~~~~~~~~~~$

#### 3. OpenVPN installing

For installing OpenVPN in the corresponding instance (HOL02-VPN) it is needed to get into the instance and install the OpenVPN with the corresponding commands.

![Installing commands](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/10939d5d-0d7d-4955-95b6-f8328e8d18aa)

![Installing commands](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/78597180-22e6-4284-9795-9fb706d6d7a7)

Once the software is installed in the PC, it can be accessed by navigating to the public IP of the instance and log in using the username 'openvpn' and the password shown in the terminal.

![OpenVPN web portal](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/07b48219-2233-40e0-90fa-cc27717960bc)

![Password shown in the terminal](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/c93f94a5-aa33-46be-bab6-305b18d16010)

![OpenVPN web portal with credentials](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/9d0763ff-3fb9-4163-b2b7-3bef1bff498b)

After that, in the web interface, Network Settings must be changed, modifying the hostname to the elastic IP and also adding the subnets CIDR.

![Hostname modification to the elastic IP address](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/b9c80f0a-a6e2-48f4-b4f3-33da5e15e5c7)

![Subnets' elastic IPs adding](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/ab1aa7e0-b480-41a0-8270-b8cd6d2113a6)

Finally, it is needed to download the user-locked profile so the VPN can be activated correctly.

![User-locked profile download](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/93ff7ee1-f767-4c65-9d85-d7019776ec86)

![VPN activation](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6dcd8cbb-cbac-44fc-a808-a290b5d0a051)

$~~~~~~~~~~~$

#### 4. Nginx installation

For installing Nginx into the EC2 instance HOL02-VoilaServer, the specific commands for Linux 2 software are applied.

![Nginx commands](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/20542f3c-495e-4d10-9a68-5ef69212160c)


![Nginx commands](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/59c95367-5459-449c-b98e-2a5be6cc8c9c)

$~~~~~~~~~~~$

#### 5. Python and Jupyter installation

Python and Jupyter must be installed in the Jupyter EC2 instance

![Python commands](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/40b1de82-cbaf-471f-9996-42619e41ad7c)

![Jupyter commands](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/31d546af-c0f7-4a6b-8f57-8102fb1ec757)

As it can be seen in these images, it can be accesed correctly by the Navigator and it also works correctly.

![Jupyter accesible by the web](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/91addd4d-50a2-4de0-8ac0-6386048a5bf2)

![Code example](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/53eee382-1db0-4e79-95a0-56125f48dd2b)

![Output example](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/3c45d47a-d0fb-47b4-b52a-26db15f2ddd5)


$~~~~~~~~~~~$

#### 6. CLI

For installing the Command Line Interface it is needed to install the software and then prompt in the terminal the WAS credentials and token.

![CLI Setup Installer](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/12d68ad4-aa0e-4e1c-9371-6a2ab22a19a0)

![AWS Credential Request](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/23513f29-9b4c-472d-be8c-2acf4c420b6b)

![AWS Credentials checking](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/5d890fdc-9dd2-4d10-97a9-859959d4f5f9)

![Credentials Prompt in the terminal](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/9a9e844c-9a7a-4f35-8c4e-be71f956224b)

Then, it is checked if it can read correctly a file stored in the S3 Bucket.

![Python code for reading the file located in the bucket](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/fc9b314b-f575-44b1-a22e-1d8e0cf8dd26)

![Correct reading](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/a78d4770-d1c6-4c8f-8e03-cde8b46874f4)

$~~~~~~~~~~~$

#### 7. Bucket and instances syncronization

With the aim of synchronizing the EC2 instances with the S3 bucket, the 'AWS Sync' command is applied, synchronizing all the content of the bucket with the main route of the instance. AWS Sync command is used as the 'cron' one was not clear for me at all.

![AWS Sync command](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/a8bf7863-c3f4-4649-b183-0f763544bfc8)

After the syncronization, it can be seen that in the instance directory ('ls') we can find the files that were in the Bucket.

![Instance directory content](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/1b4f70b1-b8e5-498f-ab67-e07e94036aff)

$~~~~~~~~~~~$

#### 8. Troubleshooting


- Internet Gateway Configuration:
When I encountered issues with internet connectivity in the infrastructure deployment, I checked the configuration of the Internet Gateway. Firstly, I ensured that the Internet Gateway was properly attached to the designated VPC. Then, I carefully checked the route tables associated with the subnets to confirm that they contained correct route entries directing internet-bound traffic to the Internet Gateway. Additionally, I reviewed the security group rules to verify that outbound internet traffic was allowed if necessary. By examining and adjusting these configurations, I was able to resolve the internet connectivity issues.

- Routing Table IP Configuration:
During the setup of routing tables in the infrastructure, I found some difficulties with the IP configuration that impeded network connectivity. To handle with it, I reviewed the routing table entries associated with each subnet, focusing on ensuring that the routing table entries specified the destination for internet-bound traffic. Additionally, I checked the CIDR block configurations of the subnets to prevent any possible overlap.

- Installing User Locker for VPN:
During the installation of the user locker for the VPN, I found some challenges. To tackle them, I followed the instructions provided in the exercise comments. After installation, I configured the user locker settings within the OpenVPN server to secure user authentication. I also checked the credentials provided during the user locker setup to ensure they matched those intended for authentication. Finally, I tested accessing the VPN web portal using the provided credentials to confirm the successful installation and authentication.
