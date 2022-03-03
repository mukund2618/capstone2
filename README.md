###CLOUD INFRASTRUCTURE PROVISION & MONITOR

##1.INTRODUCTION

This Case Study is my second and final declarative pipeline building a DevOps flow. I am building a CI/CD pipeline with the concepts, tools, and technologies learned during this training. The main focus of this project is to continuously make these small changes to the code, building, testing, provisioning cloud infrastructure and monitoring. 

##2.DEVOPS TOOLS & CLOUD SERVICES USED

GIT: 
Source code Management tool.
Git manage source codes written by the developers.

GIT HUB: 
Distributed version control & SCM. Git Hub tool is a centralized code repository and does version control.

JENKINS: 
Continuous Integration/Continuous Deployment tool to automate process. Jenkins run jobs which build pipeline and automate the deployment process by integrating with all kinds of tool by simply by installing relevant plugins.

CloudFormation:
CloudFormation service is used to provision infrastructure in AWS platform. In this case I am spinning up S3 bucket with a template.

CloudWatch:
CloudWatch service used for monitoring AWS cloud infrastructure.

AWS SNS:
SNS is used to send alert notifications. 


##3.DESIGN
 

Architecture Diagram

![image](https://user-images.githubusercontent.com/60556160/156586137-c18184bc-315c-465a-a32a-52616fbf3b74.png)

 
•	In this project developer write code and use code management tool to push it to centralized code repository [Git Hub].
•	Create Jenkins declarative pipeline job which get triggered when it senses push build starts and deploys provisioning infrastructure in AWS platform.
•	Monitoring configured with the running ec2 instance and its system performance watched in graphical representation. 

##4.SET UP PHASE

The required set up has been done as given below:

1.	In Amazon web services signup for an account and create an EC2 instance with below configurations.
Jenkin Server:
	Instance Type: t2.micro
	Base Image: Ubuntu Server 20.04
	Storage: 20 GB
	Access: SSH Keypair
	![image](https://user-images.githubusercontent.com/60556160/156484250-42ac3f57-cd59-48e1-8280-82179e1dc02a.png)

 
2.	Enable necessary cloud services
EC2
IAM
S3
CloudFormation
CloudWatch
![image](https://user-images.githubusercontent.com/60556160/156484300-e6007b3e-81c5-4356-a430-61aef24d6285.png)


##5.IAM ROLE CREATION
Create an IAM role with necessary permissions for EC2, S3, CloudFormation and CloudWatch access. Here I created role named “admin-tf” and attach this role with the Jenkins instance.

![image](https://user-images.githubusercontent.com/60556160/156484377-4dab8afd-5ec3-4064-aec3-1f238bb830b9.png)

![image](https://user-images.githubusercontent.com/60556160/156484486-325c8a93-11f9-4600-84ea-66de674d0c92.png)


 

Tools Installed:

	Jenkins 2.319.3
	Git 2.34.0
	aws-cli: 1.18.69

and you can check on the versions installed and service status to precheck are installations are smooth and working without any errors.






	


Steps involved in Jenkins Server setup:
•	When the ec2 instances are started up and running install git, Jenkins with necessary plugins related to git, git hub, CloudFormation.

•	After installation check the status of the services and it should be in running status.

![image](https://user-images.githubusercontent.com/60556160/156484547-946078f3-3cc1-4f28-a2c9-be86d067b034.png)



You can access your Jenkins console with your public ip of ec2 instance with default port 8080.

![image](https://user-images.githubusercontent.com/60556160/156484596-ff957381-0e49-4aa4-88d5-24089bc1512b.png)

 ##6.BUILD


1.	Create a Pipeline job in Jenkin console.

![image](https://user-images.githubusercontent.com/60556160/156484675-4a4d5a53-ab6a-4b9f-8418-b1da4dff1931.png)


 ![image](https://user-images.githubusercontent.com/60556160/156484712-2f653068-0fc8-41fa-9e0f-3d11228b3da4.png)

![image](https://user-images.githubusercontent.com/60556160/156484737-e79736af-2214-4cea-adb9-fded49736f26.png)


Through ssh login in to Jenkins server and do the below:
1.	Develop necessary codes and dependencies and push it to github repository.

2.	Login to your Github account and create a repository for this project.

 ![image](https://user-images.githubusercontent.com/60556160/156484799-a81b091c-51e3-43ff-980a-ee3593ccd6e9.png)


3.	Push the related files to your git hub repository.

![image](https://user-images.githubusercontent.com/60556160/156484844-2f1f0929-b2e1-421a-af44-2d021ff2050d.png)


4.	Integrate Jenkins to git hub repository through SCM in Jenkins pipeline.

 ![image](https://user-images.githubusercontent.com/60556160/156484882-c73664d2-b6a7-4fc5-900e-c72f3c6687f0.png)
 
 ![image](https://user-images.githubusercontent.com/60556160/156484936-dbf974fc-aa16-4bfa-bddf-d7a5a1941b3a.png)

![image](https://user-images.githubusercontent.com/60556160/156484960-8c728cd9-277c-4fbb-aba9-ffb79b0fbbae.png)



My Jenkinsfile and simplests3cft.json file screenshot for your reference.

![image](https://user-images.githubusercontent.com/60556160/156485022-d024cd6e-1402-475e-a892-75246d5159b6.png)

![image](https://user-images.githubusercontent.com/60556160/156485037-8bcc786c-c842-4149-aa6e-d5e3805eb405.png)


After the pipeline setup if you build the pipeline if everything goes well we can see the console output like the below screenshot. 

 ![image](https://user-images.githubusercontent.com/60556160/156485068-e192fd26-5aff-461b-9935-494a985ffdfd.png)

We can login to AWS console and check weather new S3 bucket with unique name created.

 ![image](https://user-images.githubusercontent.com/60556160/156485105-b9a05353-0cac-4fe9-a13a-e36a41758307.png)

##
7.LINTING
Linting Screenshot:

![image](https://user-images.githubusercontent.com/60556160/156485136-0de86b53-e9cb-49ce-9ee4-2942a3afa4eb.png)

Jenkins is trying to search for file in wrong server and the same corrected.

 ![image](https://user-images.githubusercontent.com/60556160/156485154-06dfcf83-5901-4a6a-85fa-f9bb2477c039.png)


You can see from the above image Jenkins configured to go and search in the right server where the file resides.

##8.MONITORING

AWS Services to be enabled:

CloudWatch

SNS

Cloudwatch:

Install CloudWatch agent in the AWS resource you need to monitor.

•	Attach an IAM role to the EC2 instance that includes the following policies:

CloudWatchAgentServerPolicy: This policy enables the EC2 instance to push the logs and metrics to the Amazon CloudWatch service.

AmazonSSMManagedInstanceCore: This policy enables the EC2 instance to read parameters stored in the SSM parameter store and to have them registered under the SSM managed instances, so you can Run Commands against it.
               
	Ensure that the SSM agent is installed in this EC2 instance.
Configure the CloudWatch Agent:
       Once the agent is installed, the next step is to configure it to push the logs           and metrics to CloudWatch.
       To configure the CloudWatch agent, you need to create a configuration file. You can create it by running the CloudWatch Agent Configuration Wizard, which you can start by        entering the following command:
               
	       sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
	       
Configure SNS for notification. 

	So whenever my instance CPU utilization go over 5% I will receive email notification.



•	Tested the server performance and stress test using yes command.

![image](https://user-images.githubusercontent.com/60556160/156485347-9643b2ac-f11b-4f96-b944-aae22b183bb3.png)


•	Misconfigured jenkinsfile and tested in pipeline built.

•	Tested end to end CI/CD pipeline build and the infrastructure provisioning successfully.


##9.CHALLENGES


During repeat pipeline build process I see the s3 bucket provisioned successfully but output throws error which describes the stack already exists.

![image](https://user-images.githubusercontent.com/60556160/156485419-7728c9eb-4248-4d2f-9703-a4939bec3236.png)

   


The same error corrected by adding “date” format of CloudFormation script line in Jenkinsfile.

![image](https://user-images.githubusercontent.com/60556160/156485446-d575f8d5-cee0-4316-b07e-d1094bb0bab7.png)

##10.IMPROVISATION

 In EC2 instance whenever I restart production server the public ip changes and the CI/CD pipeline job fails. To overcome this issue, I improvised assigning elastic Ip in AWS environment. 


                                        









