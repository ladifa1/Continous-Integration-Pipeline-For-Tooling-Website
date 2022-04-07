# CONTINOUS INTERGRATION PIPELINE FOR TOOLING WEBSITE

Create an Ubuntu instance with tcp port 8080 open

![](images/1.png)

Update Ubuntu

`sudo apt update`

![](images/2.png)

Install JDK

`sudo apt install default-jdk-headless`

![](images/3.png)

Install Jenkins

`wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -`

`sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \ /etc/apt/sources.list.d/jenkins.list'`

`sudo apt update`

`sudo apt-get install jenkins`

![](images/4.png)

![](images/5.png)

![](images/6.png)

Verify Jenkins is running 

`sudo systemctl status jenkins`

![](images/7.png)

Setup Jenkins via web using port 8080

![](images/8.png)

Get administrator password from local server

`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`

Configure Jenkins to retrieve source codes from GitHub

![](images/10.png)


Build job

![](images/11.png)

Configure Jenkins to retrieve source codes from GitHub using Webhooks

![](images/9.png)

Add build trigger by selecting "github hook trigger for GITSCM poling"

Add post-build Actions by selecting "archicve the artifacts" set ** as files to archive 

Build job by commiting changes to github repository 

![](images/12.png)

Artifacts are stored on Jenkins server locally

`ls /var/lib/jenkins/jobs/tooling_github/builds/<build_number>/archive/` 

![](images/13.png)

## Configure Jenkins to copy files to NFS server via SSH

Install "Publish Over SSH" plugin

![](images/14.png)

Configure the job to copy artifacts over to NFS server by adding pem key of instance

![](images/15.png)

![](images/16.png)

Configure Job post-build Actions by selecting "send build artifacts over SSH"

Build job by commiting changes to github repository 

![](images/17.png)

![](images/18.png)

Verify files were updated in local server 

`cat /mnt/apps/README.md`

![](images/19.png)

![](images/20.png)