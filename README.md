# AWS-Jenkins-Pipeline-SonarQube-Docker-Deployment
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

# Part 1 - Jenkins - Github Setup

SSH this cmd to get access to the Jenkins server(Use the instance public Ip as per intance generated)

ssh -i SSH-Key-Jenkins.pem ubuntu@52.23.182.224

![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/a01625e3-f8fe-4eb1-a809-6b425fc81e08)


sudo apt update

sudo apt install openjdk-11-jre

Then follow jenkins installation for Debian Ubuntu

Now expose the port 8080 on jenkins ec2 instance -> Go to Security and edit inbound rules
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/b1758794-97d3-45f7-b40d-61936d7cd02a)

Copy the admin token
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/185eebce-e2d3-4b67-8730-9b02671552df)

Now open the public ip with port - http://52.23.182.224:8080/ - and enter the token copied
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

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Part 2 - SonarQube Setup

Log into the ssh for the SonarQube Instance

SSH this cmd to get access to the SonarQube server(Use the instance public Ip as per intance generated) - PublicIP - 3.84.220.33

ssh -i SSH-Key-Jenkins.pem ubuntu@54.221.137.114

![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/7a0186c1-98f9-4b9b-914f-742191f67d17)

sudo apt update

sudo apt install openjdk-17-jre

Download SonarQube using wget method and paste the download link

wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.1.0.73491.zip
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/1e6b131b-2030-4532-aa95-4151384433fe)


sudo apt install unzip

unzip sonarqube-10.1.0.73491.zip

![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/2f050cbe-c7e9-469d-84f0-4badcc812a06)

Open the sonarqube instance with its public ip and its port- Use admin and admin for username and pass
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/b53a2b39-9f9d-41af-8791-7dc22c716fa3)

![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/1ca928ee-dcf3-4fed-83da-4c3b0a8e865c)

Create a project
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/746c8b2f-1617-47fd-bbfa-bdd8271d9f77)

![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/8f78eea9-4604-46cc-b415-6b0873d81027)

Create a global token
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/3591ddb4-4cf7-4f2b-9c5e-3ca9d140af07)

Go to Jenkins manage Plugins and install SonarQube Scanner and SSH2 Easy plugin
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/cae44fc2-c8df-4349-9d76-82c34b52f183)
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/3ecc1fdf-ac41-4048-8675-c8d88f26608a)

Now in the configure tools add the SonarQube Scanner 
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/2633dbc6-e2f6-4968-8205-4e33c6a682c1)

Go to configure systems and add the sonarqube server and paste the sonarqube url - http://54.221.137.114:9000/
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/6ca18173-3faf-4e03-b07f-143973ce9c0d)

Configure the project key in the sonarqube build steps
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/d28352a1-6be5-4da2-9255-b6b013168abd)

Add the token in the secret text dropdown under secret
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/b55bce17-e0dd-475c-9a5d-4e1a9af2006a)

Then select the created token
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/97732f54-021c-4c51-8f63-19cf49015a12)

Build and check the sonarqube report
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/1e720273-03d0-4131-b274-aae9170c16f9)

![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/45bd2c03-8fae-4fbe-9ac0-ef6fd244c5d5)

It is passed 
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/f71a06fe-eff2-4eb9-bc93-2a90849c86d1)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Part 3  - Deploy on Docker

Log into the docker ec2 instance
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/b832ad70-a547-486e-b223-34f89a3a3f75)

Install the docker from documention and add the credentials created and add the Docker group in jenkins
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/fcb56fc7-701b-4634-a150-9c0379e90432)

Add the docker Server in jenkins
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/243c09be-8f0d-4c41-88d3-b7fd3a458a31)

Under the build steps chose the remote shell build step - and add a text file just to verify
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/42046e96-2b31-46cb-8990-bd81457f42ce)

Now build the pipeline and verify if the text file is created in the docker server
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/45feebea-f6cc-4099-afd5-211246056c83)

Create a dockerfile with Nginx image and store in repository also create a folder in docker 

Add a build step execute shell - copy the contents to a location created in docker folder (scp ./* ubuntu@54.81.5.217:~/website/)
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/e800cd73-ba47-48be-b5ed-869e8dccc2a8)

Make sure the docker is given permissions to run the cmds
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/e0cdf990-e180-4ed6-a0d2-6f38370c155e)

Now in Jenkins in the build step add the remote shell content

![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/7e9067ed-77fe-4361-b23e-6abd1867a779)

Check the container working
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/311cbde3-d27d-4b6a-b5e4-dc2b2bcc99a0)

Configure the ports 8085 and website is deployed with docker container - http://54.81.5.217:8085/
![image](https://github.com/Skillz619/AWS-Jenkins-Sonarqube-Docker/assets/43133388/ea1048d3-ba1a-4d05-81ca-41f506cafa04)




