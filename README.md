# AWS-Jenkins-CI-CD-Pipeline-
![JEnkins Cicd Pipeline](https://github.com/Skillz619/AWS-Jenkins-CI-CD-Pipeline-/assets/43133388/dc71830e-2a2f-41e2-94db-962f4c98d2da)

AWS Create 3 EC2 instances
Step 1 - We will push the code the github
Step 2 - Pull the code through jenkins 
Step 3 - Test the code via sonarqube - scans
Step 4 - Deploy in Docker

# Open AWS console
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/d392d8f8-5b9d-444b-9c61-ba4f28728bf5)

Create an EC2 Instance for Jenkins with  a key pair

Create an EC2 Instance for SonarQube and use the same key pair generated

Create an EC2 Instance for Docker and use the same key pair generated

![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/2a53c25b-0add-4e94-acdb-3d033ec1eaba)

SSH this cmd to get access to the Jenkins server(Use the instance public Ip as per intance generated)

ssh -i SSH-Key-Jenkins.pem ubuntu@34.224.39.140

sudo apt update

sudo apt install openjdk-11-jre

Then follow jenkins installation for Debian Ubuntu

Now expose the port 8080 on jenkins ec2 instance -> Go to Security and edit inbound rules
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/b1758794-97d3-45f7-b40d-61936d7cd02a)

Copy the admin token
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/185eebce-e2d3-4b67-8730-9b02671552df)

Now open the public ip with port - http://34.224.39.140:8080/ - and enter the token copied
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/6e37e326-4a02-4669-b366-ff8b77db84f6)

Install the suggested plugins
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/320970c9-eb82-4a95-8826-15065b8711d1)

Create a User
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/45bf9458-bbbc-4fb4-a9d8-d4215a19de4c)

![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/7417c226-f4f9-444a-b12e-11299668fc78)

Create a Pipeline
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/b911aad7-7bc0-4b82-85e3-b8834e5ccba4)

Add the Git repo URL in the Configuration
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/a9df0413-c788-4468-abfc-d7b1f4f96ff2)

Also select GITScm to automatically triger the pipeline whenver we make changes in the repository
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/3f383fe5-877f-4fa7-9be6-a6c418c77df0)

Add the Github Webhook in the github rep settings - Add the Jenkins url ip and port (http://34.224.39.140:8080/) and select ind events - pull reqs and pushes
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/2c49a21c-a4cd-499e-9404-3cfe28d7cd4f)

File updated in workspace
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/63fc74d6-a66b-4fc9-8179-fc5e44ee3e81)

Also latest build log updated
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/fc716e33-a846-4bb3-8d84-a90bcb6c257d)


# Part 1 Summary 

We have automated the process till the Jenkins whenever we change or add the code in github repository it will trigger the jenkins automatically and Jenkins will pull automatically from the github


