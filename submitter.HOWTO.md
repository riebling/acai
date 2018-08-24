### Submitter HOWTO

![AGS Diagram](TPZ_SCOTT_Presentation_SCS_24Jul2018.png)

Git clone & use base code from [Cameron's example repo](https://github.com/11-791SoftwareEngineeringForIT/Project0), which has hard coded [several variables](https://github.com/11-791SoftwareEngineeringForIT/Project0/blob/master/submitter/submitter.sh#L23-L29) for us:
```
    # Module / task specific fields
    # Task Id and TPZ key from https://theproject.zone/f18-11791/pi0/tasks/hello-world
    semester="f18"
    courseId="11791"
    projectId="pi0"
    taskId="hello-world"
tpz_key="KMZL8VGavxwtkXp1DrsjLEKXfoOBuhGJ"
```

Supply some variables on command line:
```
export TPZ_USERNAME=er1k@andrew.cmu.edu
```
Get the submission code from the F18-11791 prototype [TPZ page](https://theproject.zone/f18-11791/pi0) (click "Get Submission Password" button, copy paste)
```
export TPZ_PASSWORD=H6CmXQOGRc34zRYyKzIa9y
```
Run the submitter script
```
er1k@islpc22:~/ACAI/Project0/submitter$ ./submitter.sh
####################
# INTEGRITY PLEDGE #
####################
Have you cited all the reference sources (both people and websites) in the file named 'references'? (Type "I AGREE" to continue). By typing "I AGREE", you agree that you have not cheated in any way when completing this project. Cheating can lead to severe consequences.
I AGREE
TODO!
Uploading answers, files larger than 5M will be ignored...
{"status":1209,"success":true,"message":"Your submission is in processing, submission token is:er1k@andrew.cmu.edu_pi0_hello-world_121\
1059739 Wait and check your code, score and feedback on TPZ."}If your submission is uploaded successfully. Log in to theproject.zone and open the submissions table to see how you did!
```
Check the TPZ submissions table page, https://theproject.zone/f18-11791/pi0/submissions - is it there? no :(

Why not? There was no data. :)  The submitter only does the following:

  * Runs a 'grade' function locally - essentially just runs the homework code
  * Creates a tarball of (output) files from the working directory
  * Uploads the tarball to TPZ AGS
  * Along with this, lots of metadata, much we don't know about:
    - andrewId
    - password
    - dns
    - semester
    - courseId
    - projectId
    - taskId
    - lan
    - tpzKey
    - feedbackId
    - codeId
    - useContainer
    - taskLimit
    - update
    - pending
    - duration
    - checkResult
    
According to [TPZ/AGS docs](https://github.com/CloudComputingCourse/TA-Manual/wiki/grader-HOWTO#enable-ags-support-for-a-task), each new Task (homework) we create requires emailing Cameron/Marshall to manually enable it by ID

Edit `submitter.sh` to update (hard-coded) `projectId` and `taskId` variables, for example
```
er1k@islpc22:~/ACAI/Project0/submitter$ diff submitter.sh submitter4.sh
27c27
<     projectId="pi0"                             # created at "Create New Project" time in TPZ
---
>     projectId="fixing-module-titles"                             # created at "Create New Project" time in TPZ
29c29
<     taskId="hello-world"                        # the same as "Slug" in the Edit Task pop-up
---
>     taskId="P4M1T1"                        # the same as "Slug" in the Edit Task pop-up
```
Presumably we DO NOT need to do what the [TPZ submitter HOWTO](https://github.com/CloudComputingCourse/TA-Manual/wiki/submitter-HOWTO#compile-the-submitter-with-docker-and-makefile) does, which is to compile the `submitter.sh` bash script into an executable, and store the compiled `submitter` executable as part of the GitHub repository given to students, and associated with the homework

## Grader HOWTO
This is more complicated. We're waiting on Cameron's [skeleton grader implementation](https://github.com/11-791SoftwareEngineeringForIT/Project0#grader) which will be hopefully much simpler than the full [TPZ/AGS implementation](https://github.com/CloudComputingCourse/TA-Manual/wiki/grader-HOWTO) that uses an Amazon Machine Image, Docker, Makefile
