# AWS Cloud Security IAM

![Project Diagram](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/CloudSecurityIAM.png) 

# In this project I will create from scratch 

* EC2 Instances
* IAM Policies
* IAM User and User Groups
* AWS Account alias
  
## 1. Launch EC2 instances 

  I'll start off by launching 2 EC2 instances. Once logged in to the AWS console I will head to the EC2 dashboard by typing in EC2 on the serch bar and clicking EC2

  ![EC2 dashboard](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/5uqIexPMUl.png)


## 2. Switch region to what is closest to me.

![region Selection](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/jSAnSpob3a.png)


* In EC2 console click on launch instances.
* In the name filed I will enter a unique name for the project. Name: (production-evelio)
* Add additional tags
        * Key: Env
        * Value: production
* I will also create a second instance and using development instead of production. (Tags will help to organize resources)

![Name and tags](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/TA4WHy8fs3.png)

* For the Amazon Machine Image(AMI) I will be using the free tier: Amazon Linux 2023 MAI and Instance Type: t2.jmicro
* I will use the default settings for the VPC and sub net.
* For storage I used 1x 8 GIB gp3.

![Successfull instance created](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/YLqpXzFnFW.png)
