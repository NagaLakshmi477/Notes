What is CI ?
It is the process of integrating the code into artifact/image continously, means when devloper do some commit, we can clone the code,install dependies,we can build the code we can scan the code we can unit testing finally we build it as image

Jenkins is the popular CI tool.
the real power lies in plugins. without plugins jenkins is web server
- If you want intergrate with git you need git pluggins
- If you want intergrate with k8s you need k8s/kubectl pluggins
- If you want to inteate with maven we need maven pluggin

Installing jenkins on AWS console
- create ec2 instance
- 
sudo curl -o /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/rpm-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/rpm-stable/jenkins.io-2023.key
sudo yum install -y fontconfig java-21-openjdk jenkins -y
sudo systemctl daemon-reload
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Shift left
===========
applictaion deploy in test,QA, UAT --> test
PROD deploy ---> testing, no scanning
we are using shift left starigy for CICD piprlines.instead of testing and scanning after deploying the application in high environement we are doing testing and scanning in Dev Environmenet. So we can find issues in early stages

Free style pipeline:
====================
- create the pipeline in UI with some clicks
1. can't restore if error comes
2. can't track no version control
3. no body remember how to do it again
4. can't resuse
5. time consuming

In jenkins everything is called Job
we have 3 stages in pipeline
1. pre-build ---> Options, envi, where to run
2. build ---> Actual pipeline
3. post-build ----> fail,sucess, notifications ....

Master Agent/Node:
==================
Jenkins has to run diffrent project pipelines,diff lang, diff versions, diff devices

jenkins master reposibility to distribute the builds to diffrent agents
we can have more agents with diff programming lang and diff OS and diff envi. so that load will be reduce on master
master collects the logs from agents

copy agent privateIp ---> jenkins --> settings ---> manage jenkins --> setup agent --> 
nodes --> configure node monitors --> checkmark all checkboxes
node --> create node --> roboshop --> checkbox --> create
remote dir --> /home/ec2-user/jenkins-agent
label ---> AGENT-1 --> only build jobs 
ssh --> paste Agent PrivateIP here 
create credenials --> with username(ec2-user) and password --> select --> host -->non verified
availabilt --> online --> apply

Now i got one error:
This agent is offline because Jenkins failed to launch the agent process on it
we need to install java here --> check java_command_not_found file

agent --> ls -l --
drwx------ 4 ec2-user ec2-user 59 Jul  2 13:20 jenkins-agent
cd jenkins-agent

drwxr-xr-x 4 ec2-user ec2-user      34 Jul  2 13:07 remoting
-rw-r--r-- 1 ec2-user ec2-user 1407936 Jul  2 12:52 remoting.jar
drwxr-xr-x 3 ec2-user ec2-user      29 Jul  2 13:20 workspace

remoting.jar
------------
- It is the Jenkins Agent software
- It is downloaded from the Jenkins controller when you connect an agent.
- It establishes a communication channel between the Jenkins controller and the agent.
 - The controller uses remoting.jar to send build instructions to the agent and receive the build results.

 workspace
 ---------
 we have our pipelines 

 POST:
 ======

 Declarative pipeline VS scripted pipeline
 ========================================

scripted pipeline is old,  Declarative pipeline is new pipeline from jenkins-2.X
scripted --> groovy based pipeline,complies at the time of execution,little bit tought but you have more control
Declarative ---> entire pipeline complies before run the pipeline,synatx is easy

we are using mix of both pipelines
 disableConcurrentBuilds() means at a time may be 2 piples are running that is we need to tell not concurent builds tells one after another build  started

parameters:
============
build with parameter ---> here we can mention our parameter hile running pipeline

Github Webhooks:
================
when devloper in feature branch when he push the code to remote i need to immidiately trigger the jenkins pipeline automatically

is any update is happen to jenkins ---> need to inform to github 
is any update is happen to github ---> need to inform to jenkins
this are called events

github jenkins webhook:
=======================
github needs to trigger the jenkins
we need to place github url to jenkins
github ---> setting ---> webhook ---> add webhook ---> playload url --> 
http://jenkins_ip:8080/github-webhook/ --> application --> json
disable --> create

now we need to change the pipeline configurations --> select github webhook trigger --> save

Now we did any code changes it automatically trigger the jenkins pipeline




 