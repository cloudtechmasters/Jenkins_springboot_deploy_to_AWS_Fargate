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

Goto Amazon Elastic Container Service --> Create cluster

<img width="1129" alt="image" src="https://user-images.githubusercontent.com/68885738/182855401-d3e76e0a-16f6-4398-b1ac-0420c9e432d9.png">

For networking keep default options:

<img width="1129" alt="image" src="https://user-images.githubusercontent.com/68885738/182855517-676c084f-5ca9-4296-a1e8-93331c7d2c03.png">

3. Create ECS service

<img width="864" alt="image" src="https://user-images.githubusercontent.com/68885738/182855842-6fa710e4-691b-410d-958b-ccc25761581d.png">

<img width="846" alt="image" src="https://user-images.githubusercontent.com/68885738/182855974-5b679a58-08d6-43a0-bfb2-1b8944a42723.png">

<img width="831" alt="image" src="https://user-images.githubusercontent.com/68885738/182856387-788c4e04-5e6f-43fa-9565-e3573996a514.png">

Deploy the service.

4. Create ECR repo:

Goto Amazon ECR --> Repositories. --> create repositories . 

Create repo with name ecs-fargate

<img width="1246" alt="image" src="https://user-images.githubusercontent.com/68885738/182856593-b25fe898-d635-4b01-b11f-033f6af519ce.png">


5. Create Jenkins pipeline Job

Goto Jenkins --> New Item

<img width="1261" alt="image" src="https://user-images.githubusercontent.com/68885738/182857272-84eba140-0ef3-45de-a8f2-e8701888f7d8.png">



    
