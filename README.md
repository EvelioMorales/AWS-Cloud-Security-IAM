# AWS Cloud Security IAM

![Project Diagram](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/CloudSecurityIAM.png) 

# In this project I will create from scratch 

* EC2 Instances
* IAM Policies
* IAM User and User Groups
* AWS Account alias

  In this scenario we are tasked with 1.Boosting computing power and 2.Onboard an intern. The intern should have teh right permission settings to contribute while keeping the company's resources secure.
  
## 1. Launch EC2 instances (Boost Computing Power)

  I'll start off by launching 2 EC2 instances. Once logged in to the AWS console I will head to the EC2 dashboard by typing in EC2 on the serch bar and clicking EC2

  ![EC2 dashboard](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/5uqIexPMUl.png)


* Switch region to what is closest to me.

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

* Once the instances are created I will check that the tags are correct

![Checking Tags](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/PITJrJRdS1.png)

## 2. Create an IAM Policy (Onboardign Intern)

* I will create an IAM(Identity Access Management) policy that gives access to the development instance
* Head to IAM console

![IAM console](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/NjTqNKBJ0f.png)

* On teh left hand select Policies
* Choose Create policy
* Switch Policy editor tab to JSON and paste the following JSON code.

```json
{    
  "Version": "2012-10-17",    
  "Statement": [        
    {            
      "Effect": "Allow",            
      "Action": "ec2:*",            
      "Resource": "*",            
      "Condition": {                
        "StringEquals": {                    
          "ec2:ResourceTag/Env": "development"                
        }            
      }        
    },        
    {            
      "Effect": "Allow",            
      "Action": "ec2:Describe*",            
      "Resource": "*"        
    },        
    {            
      "Effect": "Deny",            
      "Action": [                
        "ec2:DeleteTags",                
        "ec2:CreateTags"            
      ],            
      "Resource": "*"        
    }    
  ] 
}
```
![Paste JSON code](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/3HcMtUVMSa.png)


