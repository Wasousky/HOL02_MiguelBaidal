

## HOL 02: Deploying a hybrid infrastructure for researchers in AWS



1. configuration of the VPC, subnets, route tables, security groups, and EC2 instances.

I've created a VPC called HOL02-VPC with the address range 10.0.0.0/16.

![Captura de pantalla 2024-03-25 143302](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/11972151-05df-4456-b4ed-dc5f8f4b6812)

Within this VPC, I've set up three subnets named HOL02-DMZ, HOL02-Production, and HOL02-Research, with the IP ranges demanded in the exercise. I only include the screenshot of the creation of one of the three subnets.

![Captura de pantalla 2024-03-25 143722](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/7b6986a6-6662-4d48-84bb-ddf3472e918c)

![Captura de pantalla 2024-03-25 143950](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/d6b813f5-ba5d-4143-9f6d-9c6798f104f8)

Afterwards, I've created an Internet Gateway named HOL02-IGW and attached it to the HOL02-VPC so that it can connect to the internet.

![Captura de pantalla 2024-03-25 144839](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/5b08dcc6-4782-4e19-962a-cee4e387917b)

![Captura de pantalla 2024-03-25 144925](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/b95bbd3b-0ac1-4f9d-8939-4cf5bbe074be)

Then, I've established three route tables: HOL02-DMZ-RT, HOL02-Production-RT, and HOL02-Research-RT.

![Captura de pantalla 2024-03-25 145049](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/a7c3fdda-256c-4452-936d-e7fdc0b9bf5b)

![Captura de pantalla 2024-03-25 145358](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/363fe5db-3760-452b-906b-3e8cb615fcc4)

Each route table is associated with its respective subnet.

![Captura de pantalla 2024-03-25 145154](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/fc553448-551d-40a2-ae68-2f88e00c1cf5)

Later, I've configured three security groups:
- HOL02-DMZ-SG, that allows traffic on ports 22, 443, 943, 945, and 1194.

![Captura de pantalla 2024-04-02 145920](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6792af10-bf8f-446e-9cf0-60864309ee90)


- HOL02-Production-SG, that permits traffic on ports 80, 443, and 22 only from HOL02-DMZ-SG



- HOL02-Research-SG, that allows traffic on ports 22 and 8888 only from HOL02-DMZ-SG.

![Captura de pantalla 2024-04-02 150451](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/a315710d-ff07-486b-bf94-9c677c3e06a4)


Moreover, I've launched three EC2 instances:
![Captura de pantalla 2024-04-02 151421](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6850f58d-eb76-4459-bcda-c31b49928eef)

- HOL02-VPN is placed in HOL02-DMZ subnet using Ubuntu 22.04 LTS AMI, and it has been associated with an Elastic IP.

![Captura de pantalla 2024-04-02 145838](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/ceb615f8-e7ef-45ac-8262-91d1e9fc55d6)

![Captura de pantalla 2024-04-02 145940](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/10d00352-983e-4680-96fc-0f67cfcf2ffe)


- HOL02-VoilaServer is in HOL02-Production subnet using Amazon Linux 2 AMI.
- HOL02-Jupyter is in HOL02-Research subnet also using Amazon Linux 2 AMI.

Finally, I've created an S3 bucket named HOL02-Notebooks. All the notebooks used by the research team have been uploaded to this bucket.

![Captura de pantalla 2024-04-02 151731](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6823cdad-4d1a-480f-96b5-34b073dfb76b)



2. Import your public key to AWS EC2 and name it HOL02.

After completing the setup, I imported the public key to AWS EC2, naming it HOL02. This ensures that I can securely access my instances using SSH authentication.

![Captura de pantalla 2024-03-25 150454](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6b58aea1-bb19-4ded-a87e-f866b72d7508)

3. Moreover, to get everything correctly set, it is needed to edit the different rouying tables and apply an Internet Gateway to allow the Internet traffic.

![Captura de pantalla 2024-04-03 085952](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6fa6e475-35f8-4014-ab7d-964697299e32)



3. Get into the EC2 instance named HOL02-VPN and install the OpenVPN with the corresponding commands.

![Captura de pantalla 2024-04-02 154030](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/10939d5d-0d7d-4955-95b6-f8328e8d18aa)

![Captura de pantalla 2024-04-02 154251](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/78597180-22e6-4284-9795-9fb706d6d7a7)

Once the software is installed in the PC, it can be accessed by navigating to the public IP of the instance and log in using the username 'openvpn' and the password shown in the terminal.

![Captura de pantalla 2024-04-02 160333](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/07b48219-2233-40e0-90fa-cc27717960bc)

![Captura de pantalla 2024-04-03 090400](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/c93f94a5-aa33-46be-bab6-305b18d16010)

![Captura de pantalla 2024-04-03 090510](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/9d0763ff-3fb9-4163-b2b7-3bef1bff498b)

After that, in th web interface, Network Settings must be changed, modifying the hostname to the elastic IP and also adding the subnets CIDR.

![Captura de pantalla 2024-04-03 090603](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/b9c80f0a-a6e2-48f4-b4f3-33da5e15e5c7)

![Captura de pantalla 2024-04-03 090929](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/ab1aa7e0-b480-41a0-8270-b8cd6d2113a6)

Finally, it is needed to download the user-locked profile so the VPN can be activated correctly.

![Captura de pantalla 2024-04-03 150353](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/93ff7ee1-f767-4c65-9d85-d7019776ec86)

![Captura de pantalla 2024-04-03 150517](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6dcd8cbb-cbac-44fc-a808-a290b5d0a051)



4. Nginx installation: commands to install Nginx on the EC2 instance named HOL02-VoilaServer (Linux 2).

![Captura de pantalla 2024-04-03 152611](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/20542f3c-495e-4d10-9a68-5ef69212160c)


![Captura de pantalla 2024-04-03 152526](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/59c95367-5459-449c-b98e-2a5be6cc8c9c)


5. Python and Jupyter installation in the Jupyter instance.

![Captura de pantalla 2024-04-03 165336](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/40b1de82-cbaf-471f-9996-42619e41ad7c)

![Captura de pantalla 2024-04-03 170117](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/31d546af-c0f7-4a6b-8f57-8102fb1ec757)

It can be accesed by the Navigator and it works correctly.

![Captura de pantalla 2024-04-03 171322](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/91addd4d-50a2-4de0-8ac0-6386048a5bf2)

![Captura de pantalla 2024-04-03 171547](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/53eee382-1db0-4e79-95a0-56125f48dd2b)

![Captura de pantalla 2024-04-03 171601](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/3c45d47a-d0fb-47b4-b52a-26db15f2ddd5)

6. Bucket.

![Captura de pantalla 2024-04-04 155515](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/443a353a-e970-4faa-ae75-c66bfdba3ffc)


7. CLI. Use the keys of AWS and also the token.

![Captura de pantalla 2024-04-03 175626](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/12d68ad4-aa0e-4e1c-9371-6a2ab22a19a0)

![t](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/23513f29-9b4c-472d-be8c-2acf4c420b6b)

![Captura de pantalla 2024-04-04 153711](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/5d890fdc-9dd2-4d10-97a9-859959d4f5f9)

![Captura de pantalla 2024-04-04 154350](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/9a9e844c-9a7a-4f35-8c4e-be71f956224b)

Check if it can read correctly a file stored in the S3 Bucket.

![Captura de pantalla 2024-04-04 155233](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/fc9b314b-f575-44b1-a22e-1d8e0cf8dd26)

![Captura de pantalla 2024-04-04 155248](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/a78d4770-d1c6-4c8f-8e03-cde8b46874f4)


8. synchronize EC2 instances with the S3 bucket. (Not using cron, but with was sync)

![Captura de pantalla 2024-04-04 160222](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/a8bf7863-c3f4-4649-b183-0f763544bfc8)

After the syncronization it can be seen that in the instance directory there are the files that were in the Bucket.

![Captura de pantalla 2024-04-04 160433](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/1b4f70b1-b8e5-498f-ab67-e07e94036aff)

