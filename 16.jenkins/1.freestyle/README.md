# Freestyle JOB
* Graphical Jobs
From graphic UI we click on create a job and configure and run the job to see the output.
* the problem is we can have many and many job, we need to connect many jobs together manually one by one.
* For learning, understanding & exploring Jenkins purposes and understand the concept
* Not recommended in Real time now.

## Install Tools
- we need tools and plugins, we can install them through Manage jenkins.
![alt text](./img/install_tools.PNG)
- that to install tools we need plugins. By default we have just a small list of tools that we can install like JDK, Maven, Git, Gradle but if we want more we need to install plugins 
* Install JDK 11 tool
- Click Add JDK
- SSH into EC2 instance where jenkins is installed and get jdk 11 path 
JDK are installed under /usr/lib/jvm/
```
$ ls /usr/lib/jvm/
$ ls /usr/lib/jvm/java-1.11.0-openjdk-amd64
$ cd java-1.11.0-openjdk-amd64$
$ pwd
/usr/lib/jvm/java-1.11.0-openjdk-amd64
```
![alt text](./img/install_jdk.PNG)
* Install JDK8 tool
- Install Open JDK 8 on ec2 instance
```
$ sudo apt update
$ sudo apt install openjdk-8-jdk -y
$ ls /usr/lib/jvm/
$ cd java-1.8.0-openjdk-amd64
$ pwd
/usr/lib/jvm/java-1.8.0-openjdk-amd64
```
![alt text](./img/install_jdk_8.PNG)
* Install Maven tool
- Click Add Maven button
![alt text](./img/install_maven_tool.PNG)
* Save
* You can check installed tools by clicking on the same buttons Manage jenkis , tools
and check each installation.
* For git tool, it is already installed by default in jenkins if it is installed on ubuntu OS.

## Create Jobs
We will create a sample job to execute some shell commands.
* Step 1
![alt text](./img/create_job_1.PNG)
* Step 2
![alt text](./img/create_job_2.PNG)
* Step 3
![alt text](./img/create_job_3.PNG)
* Step 4
![alt text](./img/create_job_4.PNG)
* Step 5
![alt text](./img/create_job_5.PNG)
* Step 6
![alt text](./img/create_job_6.PNG)
* Step 7
![alt text](./img/create_job_7.PNG)
* Step 8: Check workspace of the job. normally if there is a file generated with the job it will be shown under workspace section of the job.
![alt text](./img/create_job_8.PNG)
* Step 9
![alt text](./img/create_job_9.PNG)
* Step 10
![alt text](./img/create_job_10.PNG)
* Step 11
![alt text](./img/create_job_11.PNG)
* Step 12
![alt text](./img/create_job_12.PNG)
* Step 13
![alt text](./img/create_job_13.PNG)

## Create Job for git
* Create freestyle job with name BuildGitVprofile
* Step 1: choose the jdk tool
![alt text](./img/git_job_1.PNG)
* Step 2: specify the source code repository url. we can change the cridentials or specify ssh config.
![alt text](./img/git_job_2.PNG)
* Step 3: define the build step of maven
![alt text](./img/git_job_3.PNG)
* Step 4: choose the jdk oracle 11 and save and after that run a new build.
![alt text](./img/git_job_4.PNG)
 The build takes lots of time because of the instance type t2.micro. we need to change the instance type. Then stop the instance and if it takes lots of time to stop then force stop the instance.
* Step 5: change instance type.
![alt text](./img/git_job_5.PNG)
* Step 6: choose instance type t2.small
![alt text](./img/git_job_6.PNG)
* Step 7: restart the instance and copy public id and access jenkins from the browser using the same user/password. Nothing was lost even the config, jobs still the same.
![alt text](./img/git_job_7.PNG)
* Step 8: The build is finished with success
![alt text](./img/git_job_8.PNG)
* Step 9: we see the build result. In target folder there is the war file of the project. we can remove the content of the workspace of the job by clicking on the button "Wipe Out Current Workspace".
![alt text](./img/git_job_9.PNG)
* Step 10: click configure, and post-build action and specify a reg exp for the artifactory file to save.
![alt text](./img/git_job_10.PNG)
* Step 11: click build now and after build finish click on build id to see the result.
![alt text](./img/git_job_11.PNG)
* Step 12: the artifactory is displayed and it will not be removed if we clean the workspace of the job.
![alt text](./img/git_job_12.PNG)

## Copy Job from other one and use a default took already installed on jenkins server
* Step 1: Put A name for the new job
![alt text](./img/git_job_copy1.PNG)
* Step 2: write previous job name in search input. It will appear in the result and select it
![alt text](./img/git_job_copy2.PNG)
* Step 3: use maven default
![alt text](./img/git_job_copy3.PNG)
* Step 4: Job failure because of not found mvn command
![alt text](./img/git_job_copy4.PNG)
* Step 5: Intall maven on jenkins
![alt text](./img/git_job_copy5.PNG)
* Step 6: check maven version
![alt text](./img/git_job_copy6.PNG)
* Step 7
![alt text](./img/git_job_copy7.PNG)

## Jenkins Environment Variables
In this lecture we will see three types of jenkins environment variables:
* Default jenkins variables: like BUILD_ID
* Parameter variables
* Plugin variables.

## Job versioning builds
* Step 1: create new freestyle job named "versioning-builds" copy from "BuildGitVprofile".
* Step 2: remove copied post build action
* Step 3: create new build step "Execute shell".
Jenkins Environment variables: https://wiki.jenkins.io/display/JENKINS/Building+a+software+project
Save and start build the job two times.
![alt text](./img/versions_1.PNG)
This is the result. Two war files copied to versions folder.
![alt text](./img/versions_2.PNG)
* Step 4: Make the project parameterized.
Add a String parameter.
![alt text](./img/versions_3.PNG)
User the version parameter in execute shell build step.
![alt text](./img/versions_4.PNG)
Now we don't have anymore the button "build now" but we have new button "build with parameters".
![alt text](./img/versions_5.PNG)
The result:
![alt text](./img/versions_6.PNG)
* Step 5: Add plugin
![alt text](./img/versions_7.PNG)
![alt text](./img/versions_8.PNG)
* Step 6: Install Zentimestamp
![alt text](./img/versions_9.PNG)
* Step 7: Change date pattern for BUILD_TIMESTAMP variable for our job and use it.
![alt text](./img/versions_10.PNG)
Use the BUILD_TIMESTAMP variable.
![alt text](./img/versions_11.PNG)
Don't forget to uncheck the checkbox "This project is parameterized" to not have anymore to set the variable VERSION manally.
Build Now the job and check the result.
![alt text](./img/versions_12.PNG)


