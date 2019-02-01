# acai
Notebook for ramping up on ACAI project

### Tasks

  1. Meet with Eric Nyberg for Overview *DONE*
  2. Meet Cameron Dashti for intro to The Project Zone *DONE*
  3. Current task: read through TA materials on TPZ wiki : 40% complete *DONE*
  4. Meet Eric & Boyue to discuss running his ACAI container in TPZ *DONE*
  5. lots of trying and lots of failures running Boyue's code in an Amazon VM (see http://github.com/liboyue/BOOM issues)
  6. Cameron supplies template for submitter (grader to come) *DONE*

## terminology
```
ENA, ENI - Elastic Network Adapter, Elastic Network Interface  
HVM - Hardware Virtual Machine
AGS - auto grader system (?)
EMR - elastic map reduce
Kubernetes - Tool to scale, deploy lots of containers
Terraform - Provision dependencies in cloud (like Vagrant/Chef/Puppet)
primer = ?
MOSS - "measure of software similarity" cheat detection for code
```

## Submitting Code to Autograder
File structure needs to be observed for certain required elements;  
These go into a tarball and are uploaded to TPZ
Data goes into well-known Amazon S3 buckets e.g. `S3://cmucc-code/s18/15719/spark-etl/`

## AssessMes (quizzes) [HOWTO](https://github.com/CloudComputingCourse/TA-Manual/wiki/AssessMe-HOWTO)
Done using [TPZ Assessment Portal](https://assessme.theproject.zone/admin/assessment/assessment/)  
Sets of 3 subsets of 3 similar questions (to discourage brute forcing)

## TPJ - The Project Zone
 * Logging into TPZ uses CMU/Andrew authentication rather than it's own username+password, but because it used to, signing in can be problematic, for example when creating AssessMe quizzes
 
### A TPZ "Writeup" - instructional materials
 * Lives in folder e.g: `Project/writeup-xxx/010_writeup_name.md`
### TPZ Submissions
 * Require a password, generated on TPZ site (page?)

## AWS stuff
 * The linux API to AWS EC2 is a command 'aws'. It's essential, and useful, but overloaded. There are 155 subcommands, or "things you can do" with `ami`
 * Master AWS account (root user) uses IAM (Identity Access Manager) roles to grant sub-account permissions 
  - the ways you log into AWS differ for master vs. IAM accounts, root user cannot switch roles
### Random Notes/Questions
Q: How to know what's already running in the cloud to submit for autograder?

N: cloud computing course uses `us-east-1`

# What All is Needed to Submit to Autograder

Process happens in 2 steps: submitter, checker

 * TPZ accounts (faculty / staff / students)
   - TPZ_USERNAME
   - TPZ_PASSWORD
 * Andrew ID
 * Course ID within TPZ, e.g. we have `F18: Design & Engineering of Intelligent Information Systems`  
   `F18 11-791 Design & Engineering of Intelligent Information Systems`
   - Projects within TPZ
     - Module (homework) within TPZ
       - Open time
       - Deadline
       - Writeup
       - (optional) AssessMe
       - generated TPZ Submission Password
  * AWS accounts (faculty / staff / students)
    - IAM Users
    - Policies for users, e.g TPS staff needs to set us up with[AmazonEC2ContainerRegistryReadOnly](https://docs.aws.amazon.com/AmazonECR/latest/userguide/ecr_managed_policies.html#AmazonEC2ContainerRegistryReadOnly) policy
    - a profile with role set up `AWS_PROFILE=assumed_role` so as to be able to run  
    ```
    eval $(aws ecr get-login --no-include-email --region us-east-1)
    docker pull 939223853384.dkr.ecr.us-east-1.amazonaws.com/cmucc/ags:ubuntu
    docker tag 939223853384.dkr.ecr.us-east-1.amazonaws.com/cmucc/ags:ubuntu cmucc/ags:ubuntu
    ```
  * a `submitter/` folder (where does this need to be, where does it run?)
    - `Makefile`
    - `SHC_DOCKER_IMAGE=cumcc/shc` (what/where is this exactly?)
    - `SUBMITTER_NAME=submitter` and corresponding `submitter/submitter.sh`
    - `CHECKER_NAME=checker` and corresponding `submitter/checker.sh`
  * a `grader/` folder (when, where, and by whom does this need to be / run?)
    - Makefile
    - ags-image-pull.sh
    - pom.xml
  * we have to write our own submitter and checker code (in Java?)
    - a local copy of the AGS Docker image
    - Submitter [Submitter HowTo](https://github.com/CloudComputingCourse/TA-Manual/wiki/submitter-HOWTO) mentions "Compile the Submitter with Docker and Makefile", which is very confusing. It talks about cloning the `shc` git repo, building it, running it to turn `submitter.sh` (do we have to write this?) into `submitter.sh.x.c` - it shows some example code that does not seem to have anything to do with Docker or Makefile. This seems like notes or "extra things to remember" regarding a Submitter, but not at all a tutorial or step-by-step example on how to actually create and use Submitters.
  * Grader [grader HOWTO](https://github.com/CloudComputingCourse/TA-Manual/wiki/grader-HOWTO)
    - seems like developing a grader is it's own project, with learning curve, iterative development, testing, before deplying:
    - There are so many prerequisites just to develop a grader, including use cases of
     * download, set up, and run AGS image locally as a Docker container
     * develop Java grader
     * run interactively
     * evaluate results:
       - feedback
       - log
       - score
     * practice submitting
     * validate submissions
     * run non-interactively
     * reproduce AGS 'as any student'
     * check environment
     * this gem: "For detailed usage, read the src code. The learning curve requires: Docker, Makefile, AWS Assume Role (to auth aws ecr and pull AGS image)
    
  * a submission tarball (`submission.tar.gz`) with required structure:
    -?
  * Maven
    - [Maven Upload Grader plugin](https://github.com/CloudComputingCourse/CloudComputingUtils/wiki/Plugin-Usage) <- Permission to view this requires TAs GitHub accounts be added by Cameron Dashti cdashti1@andrew.cmu.edu (c-n-d on GitHub)
    
  * Java Grader `java_grader.jar`
  * Grading rubric [example](https://github.com/CloudComputingCourse/TA-Manual/wiki/grading-rubrics-template#example)
  * `aws` command line interface
  * AGS Support for a task (what is task vs. module?) needs to be granted by TPZ staff:
    - task ID
    - `ags_policy`
    - `ags_consumer_status`
    - https://github.com/CloudComputingCourse/TA-Manual/wiki/grader-HOWTO#enable-ags-support-for-a-task
  * a grader jarfile in `target/grader.jar`
  * access to the Cloud Computing Docker Registry (or our own Docker Registry?)
    - 
  * `signature`
  * `semester`
  * `courseID` <- TPZ needs to know about this already, assuming is `11791`
  * [upload-grader-HOWTO]() <- missing


## Tricks
Cloud Computing course uses a Docker repository name like `939223853384.dkr.ecr.us-east-1.amazonaws.com` (prepending an image name like `cmucc/p0lg:v1`)

To get Markdown or YAML from a Project page on theproject.zone append to the URL ".md" or ".yaml" resulting in something that looks like yaml:
```
--- !Manifest
course: <course-id>
sections:
  - !Section
    type: writeup
    id:
    file: writeup-<module-id>/000_introduction_to_big_data_analytics.md
    title: Introduction to Big Data Analytics
  - !Section
    type: assessme
    id: 2204 # the AssessMe id
    file:
    title:
  - !Section
    type: writeup
    id:
    file: writeup-<module-id>/010_aws_emr_azure_hdinsight_and_gcp_dataproc.md
    title: AWS EMR, Azure HDInsight and GCP Dataproc
  - !Section
    type: assessme
    id: 2205
    file:
    title:
  - !Section
    type: writeup
    id:
    file: writeup-<module-id>/020_big_data_processing_and_analysis.md
    title: Big Data Processing and Analysis
  - !Section
    type: assessme
    id: 2206
    file:
    title:
  - !Section
    type: writeup
    id:
    file: writeup-<module-id>/030_project_reflection_task_mandatory_graded.md
    title: Project Reflection Task (Mandatory, graded)
  - !Section
    type: writeup
    id:
    file: writeup-<module-id>/040_project_feedback.md
    title: Project Feedback
  - !Section
    type: writeup
    id:
    file: writeup-<module-id>/050_project_discussion.md
    title: Project Discussion

module: <module-id>
```
