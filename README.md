
Create three EC2 instances, one for Jenkins and the other for Sonarqube and the third one for docker, using the t2.medium instance type.

    Log in to your AWS account, and navigate to the EC2 Dashboard.
    Click the "Launch Instance" button and choose the "Ubuntu Server 20.04 LTS" AMI.
    Select the t2.medium instance type, and configure the instance details as required.
    Add storage as required, and configure the security group to allow SSH access (port 22) and HTTP access (port 80).
    Review your settings and launch the instance.
    Repeat the above steps to create another EC2 instance for Sonarqube.

Installing Jenkins

  SSH into the Jenkins EC2 instance.
  Set the hostname using the command:
      
      sudo hostnamectl set-hostname jenkins.
      
   Update the packages with
      
      sudo apt update
      
   Install OpenJDK 11 with 
    
    sudo apt install openjdk-11-jre.
    
   Verify the installation with
   
    java -version.
    
   Add the Jenkins repository key with the command:
    
    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null.
    
   Add the Jenkins repository with 
   
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null.
    
   Update the packages again with
    
      sudo apt-get update
      
   Install Jenkins with 
    
      sudo apt-get install jenkins
    
   Enable and start the Jenkins service with: 
    
      sudo systemctl enable jenkins 
      sudo systemctl start jenkins
      
   Check the status of the Jenkins service with:
    
    sudo systemctl status jenkins
    
   Retrieve the initial Jenkins password with 
    
    cat /var/lib/jenkins/secrets/initialAdminPassword.
    Access Jenkins in your browser at https://jenkins-ec2-ip:8080
