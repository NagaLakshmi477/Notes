What is CI ?
It is the process of integrating the code into artifact/image continously, means when devloper do some commit, we can clone the code,install dependies,we can build the code we can scan the code we can unit testing finally we build it as image

Jenkins is the popular CI tool.
the real power lies in plugins. without plugins jenkins is web server
- If you want intergrate with git you need git pluggins
- If you want intergrate with k8s you need k8s/kubectl pluggins
- If you want to inteate with maven we need maven pluggin

# Installing Jenkins on AWS

## Create EC2 Instance

1. Create an **EC2 instance** in the AWS Console.

## Install Jenkins

Run the following commands on the EC2 instance:

```bash
sudo curl -o /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/rpm-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/rpm-stable/jenkins.io-2023.key

sudo yum install -y fontconfig java-21-openjdk jenkins

sudo systemctl daemon-reload

sudo systemctl start jenkins

sudo systemctl enable jenkins

sudo systemctl status jenkins
```

## Get the Initial Admin Password

Run:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Use the displayed password to complete the initial Jenkins setup.

# Shift Left

Normally, the application is deployed to **Test, QA, and UAT** environments for testing.

For **PROD deployment**, we perform testing, but scanning may not be performed at that stage.

We are using the **Shift Left strategy** in our CI/CD pipelines. Instead of performing testing and scanning after deploying the application to higher environments, we perform testing and scanning in the **DEV environment**.

This helps us **find and fix issues at an early stage**.


# Freestyle Pipeline

A **Freestyle Pipeline** is created in the Jenkins UI using a series of clicks and configurations.

## Disadvantages

1. We can't easily restore previous configurations if there is an error.
2. We can't track changes because there is no version control.
3. Nobody may remember how to configure it again.
4. We can't easily reuse the configuration.
5. It is time-consuming.

## Jenkins Job

In Jenkins, everything is called a **Job**.

## Three Stages in a Pipeline

We have three main stages in a pipeline:

### 1. Pre-Build

* Options
* Environment
* Where to run

### 2. Build

* The actual pipeline execution.

### 3. Post-Build

* Failure
* Success
* Notifications

# Master and Agent/Node

Jenkins needs to run different project pipelines using different programming languages, versions, devices, and environments.

The **Jenkins Controller (Master)** is responsible for distributing builds to different agents.

We can have multiple agents with different programming languages, operating systems, and environments. This helps reduce the load on the Jenkins Controller.

The **Jenkins Controller** collects logs from the agents and monitors them.
 

copy agent privateIp ---> jenkins --> settings ---> manage jenkins --> setup agent --> 
nodes --> configure node monitors --> checkmark all checkboxes
node --> create node --> roboshop --> checkbox --> create
remote dir --> /home/ec2-user/jenkins-agent
label ---> AGENT-1 --> only build jobs 
ssh --> paste Agent PrivateIP here 
create credenials --> with username(ec2-user) and password --> select --> host -->non verified
availabilt --> online --> apply

# Jenkins Agent Offline Error

We may get the following error:

```text
This agent is offline because Jenkins failed
to launch the agent process on it.
```

This happens because **Java is not installed on the Jenkins agent**.

Check the error log for:

```text
java_command_not_found
```

## Install Java on the Agent

We need to install Java on the Jenkins agent.

## Check Jenkins Agent Directory

On the agent, run:

```bash
ls -l
```

We can see the `jenkins-agent` directory:

```text
drwx------ 4 ec2-user ec2-user 59 Jul  2 13:20 jenkins-agent
```

Go inside the directory:

```bash
cd jenkins-agent
```

We can see the following files and directories:

```text
drwxr-xr-x 4 ec2-user ec2-user      34 Jul  2 13:07 remoting
-rw-r--r-- 1 ec2-user ec2-user 1407936 Jul  2 12:52 remoting.jar
drwxr-xr-x 3 ec2-user ec2-user      29 Jul  2 13:20 workspace
```

The `remoting.jar` file is used by Jenkins to establish communication between the **Jenkins Controller** and the **Agent**.

## `remoting.jar`

* It is the **Jenkins Agent software**.
* It is downloaded from the **Jenkins Controller** when you connect an agent.
* It establishes a **communication channel** between the Jenkins Controller and the Agent.
* The Controller uses `remoting.jar` to send build instructions to the Agent and receive the build results.
## Workspace

The **workspace** is the directory where our pipeline runs and where the pipeline's files are stored during execution.


## Declarative Pipeline vs Scripted Pipeline

**Scripted Pipeline** is the older pipeline style, while **Declarative Pipeline** was introduced with Jenkins 2.x.

### Scripted Pipeline

* It is **Groovy-based**.
* It is compiled/interpreted during pipeline execution.
* It is a little more difficult to write.
* It provides **more control and flexibility**.

### Declarative Pipeline

* The pipeline structure is validated before execution.
* The syntax is easier to understand and write.
* It provides a more structured way to define pipelines.

We are using a **mix of both Declarative and Scripted Pipelines**.

## `disableConcurrentBuilds()`

`disableConcurrentBuilds()` prevents multiple builds of the same Jenkins job from running at the same time.

For example, if one build is already running, the next build will wait until the previous build is completed.

This ensures that builds run **one after another** instead of concurrently.


# Parameters

**Build with Parameters** → Here, we can provide parameters while running the pipeline.

# GitHub Webhooks

When a developer pushes code from a **feature branch** to the remote repository, we want to immediately trigger the Jenkins pipeline automatically.

If an update happens in **Jenkins**, Jenkins needs to inform GitHub.

If an update happens in **GitHub**, GitHub needs to inform Jenkins.

These are called **events/webhooks**.


# GitHub Jenkins Webhook

GitHub needs to trigger Jenkins automatically when there is a code change.

We need to configure the **GitHub webhook URL** in GitHub.

## Configure Webhook in GitHub

Go to:

**GitHub → Settings → Webhooks → Add Webhook**

### Payload URL

Enter:

```text
http://jenkins_ip:8080/github-webhook/
```

### Content Type

Select:

**application/json**

Disable SSL verification if required.

Click **Create Webhook**.

## Configure Jenkins

Now we need to change the pipeline configuration:

**Jenkins → Pipeline → Configure → Build Triggers → GitHub hook trigger for GITScm polling → Save**

Now, whenever we make a code change and push it to GitHub, the **Jenkins pipeline will be triggered automatically**.







 