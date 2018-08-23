### Submitter HOWTO

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
