<h1> DevOps Project: Integrating SonarQube with Jenkins using Github Webhook </h1>

<h2> This is a simple DevOps project that shows how to integrate SonarQube with Jenkins using Github webhook triggering. This project creates two EC2 instances, one for Jenkins and the other for Sonarqube. </h2>

Prerequisites

   <ul> AWS account </ul>
   <ul>  Basic knowledge of Jenkins, SonarQube, and Github </ul>

Instructions

    Create two EC2 instances, one for Jenkins and the other for Sonarqube, using t2.medium instance type.
    

SSH into Jenkins EC2 instance and install Jenkins:

        sudo hostnamectl set-hostname jenkins 
        /bin/bash 
        sudo apt update 
        sudo apt install openjdk-11-jre java -version 
        curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
          /usr/share/keyrings/jenkins-keyring.asc > /dev/null 
        echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
          https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
          /etc/apt/sources.list.d/jenkins.list > /dev/null 
        sudo apt-get update 
        sudo apt-get install jenkins 


Start Jenkins:

        sudo systemctl enable jenkins 
        sudo systemctl start jenkins 

    Check Jenkins status:

        sudo systemctl status jenkins 

Retrieve Jenkins initial password:

        cat /var/lib/jenkins/secrets/initialAdminPassword 

Open Jenkins in the browser using the following URL format:

        https://jenkins-ec2-ip:8080
    
Create a new freestyle project, and under the SCM option, copy and paste the repository "HTTPS" URL from the Repository to the SCM Repository URL, and input the correct branch.

Check "GitHub hook trigger for GITScm polling". This will trigger the pipeline automatically when a change is made to the repository.

On Github, go to the repository settings and select "webhooks". Enter the Jenkins URL in the Payload URL textbox in the format http://jenkins-ip:8080/github-webhooks.

Click on the "Let me select individual events" option and select "Pull request" and "Pushes" in the checklist made available.
    
    
SSH into Sonarqube EC2 instance and install Sonarqube:

        sudo apt update 
        sudo hostnamectl set-hostname sonarqube 
        /bin/bash 
        sudo apt install openjdk-17-jre 
        wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.1.69595.zip 
        sudo apt install unzip 
        unzip sonarqube-9.9.1.69595.zip 
        cd sonarqube-9.9.1.69595 
        cd bin 
        cd linux-x86-64 
        sonar.sh start 


 Launch SonarQube in the browser using the following URL format:
    http://sonarqube-ec2-ip:9000

That's it! You have successfully integrated SonarQube with Jenkins using Github webhook triggering.
