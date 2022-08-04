# Jenkins_springboot_deploy_to_AWS_Fargate
Jenkins_springboot_deploy_to_AWS_Fargate

To do springboot deployment on AWS ECS Fargate, assuming you have below things in place:

1. Jenkins Server
2. ECS Fargate Cluster
3. ECS service 
4. ECR Repo to store docker image

Steps:
======
1. Install Jenkins Server (I am using amzon linux 2)

a. Install Java

       # sudo yum update -y
       # sudo yum install java-17-amazon-corretto* -y
       # sudo alternatives --config java

       [root@ip-172-31-10-139 opt]# sudo alternatives --config java 

    There is 1 program that provides 'java'.

      Selection    Command
    -----------------------------------------------
    *+ 1           /usr/lib/jvm/java-17-amazon-corretto.x86_64/bin/java
      

b. Install Java

      # sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
      # rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key
      # yum install jenkins -y
      # service jenkins start

      [root@ip-172-31-10-139 opt]# service jenkins start
      Starting jenkins (via systemctl):  
                                                                 [  OK  ]


      Copy the password from "/var/lib/jenkins/secrets/initialAdminPassword"
      
c. Install Git/Maven/Docker

     # sudo yum install git maven docker -y
     # service docker start
     # chmod 777 /var/run/docker.sock
     
d. In Jenkins install plugins 

    - Amazon ECR plugin
    - Docker Pipeline
    - CloudBees AWS Credentials Plugin
    
e. Create AWS credentials for ECS in jenkins

<img width="1499" alt="image" src="https://user-images.githubusercontent.com/68885738/182845718-3d97c38f-3a58-46d7-b5b3-45a862b82faf.png">

2. Create ECS Cluster
3. Create ECS service
4. Create Jenkins pipeline Job


    
