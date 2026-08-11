Why github action over jenkins
==================================
- If code in gihub no need to manage another tool like CI
- scanning tools also can be configured along with the code in github.
    codeQL,dependabot, security token scanning, etc
- integrations are easy
- we can upload artifacts also
- we can upload some files that can be verified and approved in the deployement process

Disadvanatgse:
- single point of  failure

Diagram:
---------

GitHub Repository (Code)
        |
        | Events
        | (Push, PR, Manual, etc.)
        v
GitHub Actions Workflow
        |
        | Sends job to a Runner
        v
 -------------------------------
|         Runners              |
|------------------------------|
| 1. GitHub-hosted Runner      |
| 2. Self-hosted Runner        |
 -------------------------------
        |
        v
Executes Pipeline
(Build → Test → Deploy)
        |
        v
Logs & Status in GitHub

i have created

github(code) ---- events -----> GitHub-hosted runners
                                Self-hosted runners


- we will configure runners github will call the runners
- The runner executes the pipeline and we can see logs on github.
- we are 2 types of runners github runner and self hosted runners
- we don't use github runners beacuse of security purpose
- we will use self hosted runers
- events (push,PR,manula,new branch,new issue)


we need to create orginzation:
====================================
- create one repo
- we need to flow a synatx .github/workflows/*.yaml 

crate environement ---> setting --> envi --> DEV and prod 
conditions:
control when the step should run
concurency:
options {
    disableconcurencybuids()
}
we cannot allow multiple user run same pipeline at a time

parellel and sequential:
==========================
- bydefault github actions run the jobs in parellel. so we can create multiple jobs
- for sequential we have dependncy there is a keyword needs
Actions:
=======
plugins --> frequently used things are converted into pluggins we use the directly in the pipeline
everything is action in github workflow

next we will do
- Terraform-ec2 
how to add AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY
Terraform-ec2 --> settings ---> action secreat --> new --> name ands its values and --> save 

workflow --> list of jobs
job --> pipeline
steps --> stages
step --> stage
actios ---> pluggins
runners ---> nodes
reusbale workflow --> jenkins shared library
runner --> jenkins agent 

now we will crete terraform code for runners 
- runners
# runners


We need to configure runners
settings ---> actions --> self --> here we will select linux 
It will give all commands so we need to login to mobaxterm and run those commands inrunner
 mkdir actions-runner && cd actions-runner
curl -o actions-runner-linux-x64-2.335.1.tar.gz -L https://github.com/actions/runner/releases/download/v2.335.1/actions-runner-linux-x64-2.335.1.tar.gz
tar xzf ./actions-runner-linux-x64-2.335.1.tar.gz
 ./config.sh --url https://github.com/githut-actions/runners --token BVU3MJ2IDJ65PFYRWF3ZGVLKJUGS4    (eveytime the need take from aws)

runner groups --> default --> check box 
sudo vim /etc/systemd/system/runner.service
sudo systemctl enable runner
sudo systemctl start runner

Github Action Architecutre:
=================================

Github ----> Runner --->  --->pipelines --> It will call resusable pipeline --> reusable workflow ---> It runner will connect Amazxon Eks we are deploying on EKS
With in runner pipelines are runing

- next
robsohop-infra-dev-actions
it conatin vpc,sg,bastion,eks,ecr
we will create images using pipelin and we will push to ecr and we will deplotying using helm ekr on github actions
- catalogue -->cicd.yaml
- reusable work flow

output in this job ---> passing as input to the other job
we need to mange the outputs to use in aother jobs
docker build state:
we need to create the ECR repo
ecr --> private repo --> repositary ---> crate private repo --> roboshop/catalogue --> view push commands
on push command 3 ther is a id 
-- After the build completes, tag your image so you can push the image to this repository:
we need to give the credenatisla for docker push
settings --> action secreate --> Actions secrets and variables --> 


