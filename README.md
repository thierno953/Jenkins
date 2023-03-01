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
