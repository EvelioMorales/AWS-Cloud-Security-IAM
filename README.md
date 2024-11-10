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

### (Onboardign Intern)

## 2. Create an IAM Policy Onboardign Intern

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

* Click Create policy 


* Click next and fill in the Policy details

![Policy Details](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/Oyfd0t53kl.png)

# 3. Create an AWS Account Alias 

* Go to IAM dashboard
* On the right hand side under Account Alias click create(The Alias will re[place teh account ID which is a bunch of numbers and will make it easier for the inter to remember)

![Alias](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/vCvWmoDgRO.png)

# 4 Create IAM User and User Groups

* from the IAM dashboard click User Groups on the left hand side
* Click create user group
* To set up user group:
    * Name: dev-group
    * Attach permision policies: EnvironmentPolicy

![Environment policy](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/Bc4f1w8TNs.png)

* Now let's create a user
* Click on Users on the left hand side
* Click Create user
* Under user name: dev-evelio
* Then click on provide user access to AWS Management Console
* Then click I want to create an IAM user
* And for this project I will uncheck teh box that makes user create a new password at next sing-in and click next
* Then check the box to add to dev-group to apply security policies to user and click next 
* Then click on create user.

On the following screen the usre's log in credentials will show I have the option to email or download a file of the to send to the intern to log in. 

![log in credentials for new user](https://github.com/EvelioMorales/AWS-Cloud-Security-IAM/blob/main/VSBGqkreHC.png)

Now I open a newbrowser and log in as a new user and I will see acces denied on resources the user does not have access to. Also I can test the policy by trying to stop production instance, but an error message shows do to the policy in place but when I go to delete teh development instance I am able to stop it. That has concluded the project on creating an IAM user. Thanks!
