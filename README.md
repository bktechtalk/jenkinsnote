# jenkinsnote
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
https://dzone.com/articles/jenkins-03-configure-master-and-slave

Click on Manage Jenkins in the left corner on the Jenkins dashboard.
Click on Manage Nodes.Manage Nodes
Select New Node and enter the name of the node in the Node Name field.
Select Permanent Agent and click the OK button. Initially, you will get only one option, "Permanent Agent." Once you have one or more slaves you will get the "Copy Existing Node" option.Node options
Enter the required information.

Some required fields include:

1
Name: Name of the Slave. e.g: Test
2
​
3
Description: Description for this slave (optional). e.g: testing slave
4
​
5
# of Executors: Maximum number of Parallel builds Jenkins master perform on this slave. e.g: #2
6
​
7
Remote root directory: A slave needs to have a directory dedicated to Jenkins. Specify the path to this directory on the agent. e.g: /home/
8
​
9
Usage: Controls how Jenkins schedules builds on this node. e.g: Only build jobs with label expressions matching this node.
10
​
11
Launch method: Controls how Jenkins starts this agent. e.g: Launch agent agents via SSH
6. Enter the Hostname in the Host field.

7. Select the Add button to add credentials. and click Jenkins.

8. Enter Username, Password, ID, and Description.Fields to enter

9. Select the dropdown menu to add credentials in the Credentials field.

10. Select the next dropdown to add the Host Key Verification Strategy under Non verifying Verification Strategy.

11. Select Keep this agent online as much as possible in the Availability field.Configuration

12. Click the Save button.

Master and slave

#Start building your software project
Create a Jobs

###Jenkins “freestyle”
Jenkins “freestyle” jobs support simple continuous integration by allowing you to define sequential tasks in an application lifecycle, they do not create a persistent record of execution, enable one script to address all the steps in a complex workflow, or confer the other advantages of pipelines.

###jenkins pipelines
pipelines enable you to define the whole application lifecycle. Pipeline functionality helps Jenkins to support continuous delivery (CD). The Pipeline plugin was built with requirements for a flexible, extensible, and script-based CD workflow capability in mind.

Pipelines are Jenkins jobs enabled by the Pipeline (formerly called “workflow”) plugin and built with simple text scripts that use a Pipeline DSL (domain-specific language) based on the Groovy programming language.

###Pipeline Vocabulary
Pipeline terms such as “step,” “node,” and “stage” are a subset of the vocabulary used for Jenkins in general.

####Step
A “step” (often called a “build step”) is a single task that is part of sequence. Steps tell Jenkins what to do.

####Node
In pipeline coding contexts, as opposed to Jenkins generally, a “node” is a step that does two things, typically by enlisting help from available executors on agents:

Schedules the steps contained within it to run by adding them to the Jenkins build queue (so that as soon as an executor slot is free on a node, the appropriate steps run).

Creates a workspace, meaning a file directory specific to a particular job, where resource-intensive processing can occur without negatively impacting your pipeline performance. Workspaces last for the duration of the tasks assigned to them.

(In Jenkins generally, a “node” means any computer that is part of your Jenkins installation, whether that computer is used as a controller or as an agent).

####Stage
A “stage” is a step that calls supported APIs. Pipeline syntax is comprised of stages. Each stage can have one or more build steps within it.

Familiarity with Jenkins terms such as “controller,” “agent”, and “executor” also helps with understanding how pipelines work. These terms are not specific to pipelines:

#####controller - A “controller” is the basic installation of Jenkins on a computer; it handles tasks for your build system. Pipeline scripts are parsed on controllers, and steps wrapped in node blocks are performed on available executors.

#####agent - An “agent” (formerly "slave") is a computer set up to offload particular projects from the controller. Your configuration determines the number and scope of operations that an agent can perform. Operations are performed by executors.

#####executor - An “executor” is a computational resource for compiling code. It can run on controller or agent machines, either by itself or in parallel with other executors. Jenkins assigns a java.lang.Thread to each executor.

###Preparing Jenkins to Run Pipelines

Installing the Pipeline Plugin
 Open Jenkins in your web browser

Navigate to Manage Jenkins > Manage Plugins >Build Pipeline

####Navigate to the Available tab, filter by Build Pipeline

Select the Pipeline plugin and install

Restart Jenkins 


