# jenkinsnote
jenkins is an Open source, Java-based automation tool. This tool automates the Software Integration and delivery process called Continuous Integration and Continuous Delivery. Jenkins support various popular Version control system, Software build, and delivery tools. 
## Reset Jenkins Admin Credentails
### 1) Path to check default jenkins admin credenatils 
/var/lib/jenkins/secrets/initialAdminPassword

### 2) Path to check jenkins root configuration
/var/lib/jenkins/config.xml

### 3) If you forgot admin credentails and want to reset 
Stop Jenkins
Go go edit /var/lib/jenkins/config.xml
Change <useSecurity>true</useSecurity> to false
Restart Jenkins: sudo service jenkins restart
Navigate to the Jenkins dashboard to the "Configure Security" option you likely used before. This time, setup security the same as before, BUT set it to allow anyone to do anything, and allow user signup.

###Steps to Configure Jenkins Master and Slave Nodes
- https://dzone.com/articles/jenkins-03-configure-master-and-slave
### Pipeline Vocabulary
Pipeline terms such as “step,” “node,” and “stage” are a subset of the vocabulary used for Jenkins in general.

## Pipeline concepts
The following concepts are key aspects of Jenkins Pipeline, which tie in closely to Pipeline syntax (see the overview below).

#### Pipeline
A Pipeline is a user-defined model of a CD pipeline. A Pipeline’s code defines your entire build process, which typically includes stages for building an application, testing it and then delivering it.

Also, a pipeline block is a key part of Declarative Pipeline syntax.

### Node
A node is a machine which is part of the Jenkins environment and is capable of executing a Pipeline.
Also, a node block is a key part of Scripted Pipeline syntax.

#### Stage
A stage block defines a conceptually distinct subset of tasks performed through the entire Pipeline (e.g. "Build", "Test" and "Deploy" stages), which is used by many plugins to visualize or present Jenkins Pipeline status/progress. [6]

#### Step
A single task. Fundamentally, a step tells Jenkins what to do at a particular point in time (or "step" in the process). For example, to execute the shell command make use the sh step: sh 'make'. When a plugin extends the Pipeline DSL, [1] that typically means the plugin has implemented a new step.

### Types of Jenkins pipeline

There are two type of Jenkins pipeline based on which format the Jenkinsfile is written.

Declarative pipeline
Scripted pipeline

#### Declarative Pipeline fundamentals
The Declarative pipeline is a new feature that is added to create the pipeline. This is basically written in a Jenkinsfile which can be stored into a source code management system such as Git. 
In Declarative Pipeline syntax, the pipeline block defines all the work done throughout your entire Pipeline.

#### Start building your software project
Create a Jobs

The Agent is where the whole pipeline runs. Example, Docker. The Agent has following parameters:

any – Which mean the whole pipeline will run on any available agent.
none – Which mean all the stages under the block will have to declared with agent separately.
label –  this is just a label for the Jenkins environment
docker –  this is to run the pipeline in Docker environment.
The Declarative pipeline code will looks like this:

pipeline {
  agent { label 'node-1' }
  stages {
    stage('Source') { 
      steps {
        git 'https://github.com/digitalvarys/jenkins-tutorials.git''
      }
    }
    stage('Compile') { 
      tools {
        gradle 'gradle4'
      }
      steps {
        sh 'gradle clean compileJava test'
      }
    }
  }
}

#### Scripted Pipeline
The scripted pipeline is a traditional way of writing the Jenkins pipeline as code. 
Ideally, Scripted pipeline is written in Jenkins file on web UI of Jenkins.
Unlike Declarative pipeline, the scripted pipeline strictly uses groovy based syntax. 

Let us see the structure and syntax of the scripted pipeline

##### Node Block:
Node is the part of the Jenkins architecture where Node or agent node will run the part of the workload of the jobs and master node will handle the configuration of the job. So this will be defined in the first place as

node {
}
Stage Block:
Stage block can be a single stage or multiple as the task goes. And it may have common stages like

Cloning the code from SCM
Building the project
Running the Unit Test cases
Deploying the code
Other functional and performance tests.
So the stages can be written as mentioned below:

stage {
}
So, Together, the scripted pipeline can be written as mentioned below.

stage {
}
So, Together, the scripted pipeline can be written as mentioned below.
node ('node-1') {
  stage('Source') {
    git 'https://github.com/digitalvarys/jenkins-tutorials.git''
  }
  stage('Compile') { 
    def gradle_home = tool 'gradle4'
    sh "'${gradle_home}/bin/gradle' clean compileJava test"
  }
}

https://digitalvarys.com/jenkins-pipeline/


### Jenkins “freestyle”
Jenkins “freestyle” jobs support simple continuous integration by allowing you to define sequential tasks in an application lifecycle, they do not create a persistent record of execution, enable one script to address all the steps in a complex workflow, or confer the other advantages of pipelines.

### jenkins pipelines
pipelines enable you to define the whole application lifecycle. Pipeline functionality helps Jenkins to support continuous delivery (CD). The Pipeline plugin was built with requirements for a flexible, extensible, and script-based CD workflow capability in mind.

Pipelines are Jenkins jobs enabled by the Pipeline (formerly called “workflow”) plugin and built with simple text scripts that use a Pipeline DSL (domain-specific language) based on the Groovy programming language.

#### Preparing Jenkins to Run Pipelines Jobs

Installing the Pipeline Plugin
 Open Jenkins in your web browser

Navigate to Manage Jenkins > Manage Plugins >Build Pipeline

#### Navigate to the Available tab, filter by Build Pipeline

Select the Pipeline plugin and install

Restart Jenkins 

### Multibranch Pipeline

The Multibranch Pipeline project type enables you to implement different Jenkinsfile for different branches of the same project. In a Multibranch Pipeline project, Jenkins automatically discovers, manages and executes Pipelines for branches that contain an in-source control.

- https://www.jenkins.io/doc/book/pipeline/#scripted-pipeline-fundamentals
- https://www.jenkins.io/doc/book/pipeline/syntax/
