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

## Parameterized Jobs

- A build parameter allows us to pass data into our Jenkisn jobs. Using build parameters, we can pass any data we want: git branch name, secret credentials, hostnames and ports, and so on.
- Any Jenkins job or pipeline can be parameterized. All we need to do is check the box on the General settings tab, **This project is parameterized :**

## Parameterized Jobs Continued...

- **Type:** the data type for the parameter (string, boolean, etc.).
- **Name:** the name identifying the parameter.
- **Default value:** an optional value that will be used when a user doesn't specify one.
- **Description:** optional text that describes how the parameter is used.
- A single Jenkins job or pipeline can have multiple parameters. The only restriction is that the parameter name must be unique.

## Types of Parameters

Jenkins supports several parameter types. Bellow is a list of the most common ones, but keep in mind that different plugins may add new parameter types:

- **String:** any combination of characters and numbers.
- **Choice:** a pre-defined set of strings from which a user can pick a value.
- **Credentials:** a pre-defined Jenkins credential.
- **File:** the full path to a file on the filesystem.
- **Multi-line String:** same as String, but allows newline characters.
- **Password:** similar to the Credentials type, but allows us to pass a plain text parameter specific to the job or pipeline.
- **Run:** an absolute URL to a single run of another job.

## Jenkins pipeline

- Pipeline can be run in a loop
- It supports larger projects that may involve a high CPU job, provided the Jenkins infrastructure is scalable enough to support it.
- Since Jenkins is written in code, any number of users can use it as a template, modify it and run customized tests and processes.
- Multiple jobs can be run in parallel.
- Jenkins Pipeline is robust. Pipeline can automatically be resumed from it might have stopped for any reason.

## Understanding the pipeline

- **Pipeline** : A user-defined block, which contains all the processes such as **build**, **test**, **deploy**, etc. All the stage and steps are defined in this block.
- **Node** : The node is machine on which Jenkins runs. A node block is used in scripted pipeline syntax.
- **Stage** : This block contains a series of steps in a pipeline. i.e., **build**, **test**, **deploy** processes on a stage.

## Multiple Stages in Jenkins pipeline

```bash
pipeline {
   agent any

   stages {
      stage('build') {
         steps {
            echo 'Hello build stage'
         }
      }
      stage('test') {
         steps {
            echo 'Hello test stage'
         }
      }
      stage('deploy') {
         steps {
            echo 'Hello deploy stage'
         }
      }
   }
}
```

## Pipeline COntinued...

- **stages:**

* This section wraps all of the individual stage definitions(directives) that define the main body and logic for the pipeline.

- **steps:**

* This section wraps a set of DSL steps within a stage definition. It services to separate the collection of steps from other items within a stage, such as environment definitions.

* **posts:**

* This section wraps around steps and conditions to be done or checked at the end of a pipeline run or at the end of a stage.

#### Pipeline Example

```bash
pipeline {
   agent any

   stages {
      stage('name1') {
         steps {
            ---
         }
         post {
            ---
         }
      }
      stage('name2') {
         steps {
            ---
         }
      }
   }
   post {
      ---
   }
}
```

- **Directives**

* A directive can be thought of as a statement or block of code that does any of the following in a pipeline.

* Definies values (worker)
* Configures behavior {cron(070015)}
* Specifies actions to be done (DSL)

- **Step**

* The label steps itself is a section title with in a stage of the pipeline. However, within the section, we can have any valid DSL statement, such as git, sh, echo, etc. You can think of a step here as corresponding to one of these statements.
* **Conditionals** : Conditionals supply a condition or criteria under which an action should occur. These are optional. There are two cases you may encounter/use.

- **When** : Strictly speaking, this is a directive. It resides within a stage definition and defines criteria for whether or not a stage should be executed. For example:

```bash
stage ('build') {
   when {
      branch 'foo'
   }
   <steps>
}
```

- Conditionals blocks in the post section that define the criteria for doing post-processing. The criteria (conditions) here refer to the status of the build, such as success or failure.

```bash
pipeline
   agent
   environment
   tools
   options
   triggers
   parameters
   libraries
   stages

         stage
             agent
             environment
             tools
             steps
                 DSL statements
             post

         stage
             ---

   post
```

- **Pipeline**

* The pipeline block is required in a jenkins Declarative Pipeline. It is the outermost section and signals that this is a Pipeline project. The syntax is simple pipeline {} with the rest of the code within the closure:

```bash
pipeline {
   // pipeline code
}
```

- **agent any** : This syntax tells Jenkins that the pipeline or stage can run on any agent that is definied, without regard to what label it has.
- **agent none** : When used at the top level, this indicates that we are not specifying and agent globally for the pipeline. The implication is that an agent will be specified, if needed, for individual stages.

- **agent {label "<label>"}** : This indicates that the pipeline or stage can run on any agent that has the label <label>.

* **Enivironment**
* Jenkins Enivironment Variable is a global variable exposed through the env variable and used anywhere in the Jenkins file. Any value stored in the env variable gets stored as a String type. Enivironment Variables can be set either at the pipeline top level, at the specific stage level, or inside the script block.

```bash
environment {
         TIMEZONE = "eastern"
         TIMEZONE_DS = "${TIMEZONE}_dayligth_savings"
}
```

- **Tools**
- Jenkins users are familiar with using the Global Tool Configuration screen to configuration versions, paths, and installers for tools. Once configured there, the tools directive allows use to specify which of these we want to have auto-installed and made available in the path on the agent we've chosen.

```bash
tools {
   gradle "gradle3.2"
}
```
