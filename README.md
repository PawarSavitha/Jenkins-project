# Jenkins-project 😃 

# AWS Instance
- Go to AWS Console

- Instances(running)

- Launch instances
![image](https://github.com/PawarSavitha/Jenkins-project/assets/114134446/49911f58-2ed0-4f5f-84dc-12731a088e2b)

## Install Jenkins.
Pre-Requisites:

Java (JDK)
- Run the below commands to install Java and Jenkins

### Install Java
```
sudo apt update
sudo apt install openjdk-11-jre
```
Verify Java is Installed
```
java -version
``````
Now, you can proceed with installing Jenkins

``````
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
``````

**Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

- EC2 > Instances > Click on
- In the bottom tabs -> Click on Security
- Security groups
- Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).
![image](https://github.com/PawarSavitha/Jenkins-project/assets/114134446/f02d1199-e748-4618-bb12-dd9a1f908c16)

## Login to Jenkins using the below URL:
http://:8080 [You can get the ec2-instance-public-ip-address from your AWS EC2 console page]

Note: If you are not interested in allowing All Traffic to your EC2 instance 1. Delete the inbound traffic rule for your instance 2. Edit the inbound traffic rule to only allow custom TCP port 8080
![image](https://github.com/PawarSavitha/Jenkins-project/assets/114134446/4edb0c1a-776c-497d-96bf-a01ec250184f)

- After you login to Jenkins,
- Run the command to copy the Jenkins Admin Password
  
```
 sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
- Enter the Administrator password

![image](https://github.com/PawarSavitha/Jenkins-project/assets/114134446/155b2a76-3f99-42dc-b538-97c629f3f45c)

### Click on Install suggested plugins!

![image](https://github.com/PawarSavitha/Jenkins-project/assets/114134446/38bcfda2-a27c-4899-a887-ac0e1587961e)

### Wait for the Jenkins to Install suggested plugins

Create First Admin User or Skip the step [If you want to use this Jenkins instance for future use-cases as well, better to create admin user]
![image](https://github.com/PawarSavitha/Jenkins-project/assets/114134446/b0f419e6-39da-4135-a7d2-710a20875baa)

Jenkins Installation is Successful. You can now starting using the Jenkins

## Install the Docker Pipeline plugin in Jenkins:
Log in to Jenkins.

- Go to Manage Jenkins > Manage Plugins.

- In the Available tab, search for "Docker Pipeline".

- Select the plugin and click the Install button.

- Restart Jenkins after the plugin is installed.

- Wait for the Jenkins to be restarted.
![image](https://github.com/PawarSavitha/Jenkins-project/assets/114134446/69a58cd6-736c-4cfe-a924-8b1d3a2dd012)

## Docker Slave Configuration

Run the below command to Install Docker
``````
sudo apt update
sudo apt install docker.io
``````
## Grant Jenkins user and Ubuntu user permission to docker deamon.
```sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
``````
Once you are done with the above steps, it is better to restart Jenkins.
``````
http://<ec2-instance-public-ip>:8080/restart
``````
The docker agent configuration is now successful.

# Happy learning 🙂

