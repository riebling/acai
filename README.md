# acai
Notebook for ramping up on ACAI project

### Tasks
0 Meet with Eric Nyberg for Overview
1 Meet Cameron Dashti for intro to The Project Zone
2 Current task: read through TA materials on TPZ wiki : 40% complete
3 Meet Eric & Boyue to discuss running his ACAI container in TPZ
4 lots of trying and lots of failures running Boyue's code in an Amazon VM (see http://github.com/liboyue/BOOM issues)

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
