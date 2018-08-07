# acai
Notebook for ramping up on ACAI project

### Tasks
0 Meet with Eric Nyberg for Overview
1 Meet Cameron Dashti for intro to The Project Zone
2 Current task: read through TA materials on TPZ wiki : 20% complete

## terminology
```
ENA, ENI - Elastic Network Adapter, Elastic Network Interface  
HVM - Hardware Virtual Machine
AGS - auto grader system (?)
EMR - elastic map reduce
Kubernetes - Tool to scale, deploy lots of containers
Terraform - Provision dependencies in cloud (like Vagrant/Chef/Puppet)
primer = ?
```

## TPJ - The Project Zone
 * Logging into TPZ uses CMU/Andrew authentication rather than it's own username+password, but because it used to, signing in can be problematic, for example when creating AssessMe quizzes
 
## AWS stuff
 * The linux API to AWS EC2 is a command 'aws'. It's essential, and useful, but overloaded. There are 155 subcommands, or "things you can do" with `ami`
 
### Random Notes/Questions
How to know what's already running in the cloud to submit for autograder

## Tricks
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
