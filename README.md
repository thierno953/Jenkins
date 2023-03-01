# JENKINS

- **Jenkins** is an open-source automation tool written in java with plugins built for continuous integration. Jenkins is used to build and test your software projects continuously making it easier for developers to integrate changes to the project, and making it easier for users to obtain a fresh build. It also allows you to continuously deliver your sofware by integrating with a large number of testing and deployment technologies.

- **CI/CD** is a method to frequently delivery apps to costomers by introducing automation in the stages of continuous delivery, and continuous deployment. CI/CD is a solution to the problems integrating new code can cause for development and operations teams (AKA "integration hell")

```bash
------------------------------------|-----------------------------------------------|-------------------------------
Continuous Integration              |                Continuous Delivery            |        Continuous Deployement
------------------------------------|-----------------------------------------------|------------------------------
Build ==> Test ==> Merge        ====|====>           Automatically Release     =====|==>      Automatically Deploy
                                    |                To Repository                  |          To Production
------------------------------------|-----------------------------------------------|--------------------------------
```

## CI continued...

- Continuous integration
- Developers praticing continuous integration merge their changes back to the main branch as often as possible. The developer's changes are validated by creating a build and running automated tests against the build. By doing so, you avoid integration challenges that can happen when waiting for release day to merge changes into the release branch.
- Continuous integration puts a great emphasis on testing automation to check that the application is not broken whenever new commits are integrated into the main branch.

## CD continuous delivery...

- Continuous devlivery
- Continuous delivery is a extension of continuous integration since it automatically deploys all code changes to a testing and/or production environment afetr the build stage.
- This means that on top of automated testing, you have automated release process and you can deploy your application any time by clicking a button.

## Continuous deployment...

- Continuous deployment goes to step further than continuous delivery. With this practice, every change that passes all stages of your production pipeline is released to your customers. There's no human intervention, and only a failed test will prevent a new change to be deployed to production.
- Continuous deployment is an excellent way to accelerate the feedback loop with your customers and take pressure off the team as there isn't "release day" anymore. Developers can focus on building software, and they see their work go live minutes after they've finished working on it.

### Jenkins Standalone Architecture

```bash
Developers commit changes           <-------------------------->
----------------------------------> | Github Repository |
                                    |       |
                                    <-------------------------->
                                    |   Jenkins server
                                    | (Build<-->Test<-->Result)
                                    |       |<----------------->
                                    |       | Deploys to Production server
                                    <-------------------------->
                                    | Production server

```

### Jenkins Distributed Architecture (Master-Slave Model)

```bash
Developers commit changes           <-------------------------->
----------------------------------> | Github Repository |
                                    |       |
                                    |       | Pulls and build
                                    <-------------------------->
                                    |   Jenkins Master server
                                    | (Build<-->Test<-->Result)
                                    |       |
                                    <-------------------------->
                                         | Jenkins Slave
                                    <--------------------------->
                                    |             |             |
                                 Windows        Linux          MacOS
```

## Plugins in Jenkins

- Plugins are the primary means of enhancing the functionality of a Jenkins environment to suit organization or user-specific needs. The are over a thousand different plugins which can be installed on a Jenkins controller and to integrate various build tools, cloud providers, analysis tools, and much more.

## Types of Jenkins Job

- **Freestyle Project:**
- This job type is the default project type and is the most flexible to configure.

- **Pipeline:**
- A pipeline is a way of defining your entire build process using code in the form of a Jenkinsfile.

## Pipeline Job

```bash
pipeline {
   agent any

   stages {
      stage('Hello') {
         steps {
            echo 'Hello World'
         }
      }
   }
}
```

## Multi-Branch Pipeline

- A multi-branch pipeline is an extension of a Pipeline Job. However, it has a way of automatically creating Jenkins pipelines based on source control branches. Jenkins can then automatically discover new branches in the source control, and it can also automatically create a pipeline for that branch.

### Minimum harware requirements:

```bash
256 MB of RAM

1 GB of drive space (although 10 GB is a recommended minimum if running Jenkins as a Docker Container)
```

### Recommended hardware configuration for a small team:

```bash
4 GB+ of RAM

50 GB+ of drive space
```

### Software requirements:

- Java: see the Java Requirements page
- web browser: see the Web Browser Compatibility page
- For Linux operating system: Linux Support Policy

```bash
cat /etc/os-release
```

```bash
PRETTY_NAME="Ubuntu 22.04.1 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.1 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```

```bash
# Install Java
# To install latest OpenJDK 11
sudo apt install openjdk-11-jre
# To check the java version
java -version
```

```bash
# Add Jenkins APT Repository Key
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key |sudo gpg --dearmor -o /usr/share/keyrings/jenkins.gpg
# Append the Debian package repository address to the server's sources.list
sudo sh -c 'echo deb [signed-by=/usr/share/keyrings/jenkins.gpg] \ http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
# Run apt update so that apt will use the new repository
sudo apt update
```

### Install Jenkins and its dependencies:

```bash
sudo apt-get install jenkins
```

- Start Jenkins jenkins

```bash
sudo systemctl start jenkins
sudo systemctl status jenkins
```

- Opening the firewall

```bash
sudo ufw allow 8080
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status
```

- How to check Jenkins version command line in linux

```bash
grep version /var/lib/jenkins/config.xml

<?xml version='1.1' encoding='UTF-8'?>
   <version>2.332.3</version>
```

### Configure Jenkins on Ubuntu 22.04 LTS

- After install of Jenkins, successfully running Jenkins services and we will check on browser by jenkins default port number 8080.

```bash
http://ip_address_or_domain_name:8080
```

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
