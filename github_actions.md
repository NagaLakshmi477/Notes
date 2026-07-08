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

