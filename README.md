

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



- HOL02-Production-SG, that permits traffic on ports 80, 443, and 22 only from HOL02-DMZ-SG



- HOL02-Research-SG, that allows traffic on ports 22 and 8888 only from HOL02-DMZ-SG.



Moreover, I've launched three EC2 instances:
- HOL02-VPN is placed in HOL02-DMZ subnet using Ubuntu 22.04 LTS AMI, and it has been associated with an Elastic IP.



- HOL02-VoilaServer is in HOL02-Production subnet using Amazon Linux 2 AMI.



- HOL02-Jupyter is in HOL02-Research subnet also using Amazon Linux 2 AMI.


Finally, I've created an S3 bucket named HOL02-Notebooks. All the notebooks used by the research team have been uploaded to this bucket.





2. Import your public key to AWS EC2 and name it HOL02.

After completing the setup, I imported the public key to AWS EC2, naming it HOL02. This ensures that I can securely access my instances using SSH authentication.

![Captura de pantalla 2024-03-25 150454](https://github.com/Wasousky/HOL02_MiguelBaidal/assets/92041194/6b58aea1-bb19-4ded-a87e-f866b72d7508)



3. Third item
