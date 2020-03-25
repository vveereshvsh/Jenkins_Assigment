Setting up a CI/CD pipeline with Maven and Jenkins 
======================================================

The following document describes how to setup a CI/CD pipeline with Jenkins. The example illustrates how code changes can be built with Jenkins and deployed. It can be used as a baseline for creating more advanced pipelines that involve deploying in multiple stages (i.e. deploy to stage/production, etc).

## Prerequisites
* A jenkins server installed on local or VM machine on any cloud provider.
* Maven 3.X tool installed 
* Pipeline utility plugin, Ansible plugin
* Ansible tool installed
* Tomcat server installed and managed by ansible

## Configure Jenkins

- Install jenkins using yum command. You should be able to access Jenkins at http://35.226.157.35:8080/

- Once you are in and you're logged in, click on **Manage Jenkins**, then click on **Global Tool Configuration**

### Configure Maven

- Add Maven tool and use auto installation from Apache

- Give it a name of `maven`

### Install the Pipeline Utility plugin 

- Click on **Manage Jenkins > Manage Plugins**, click on the **Available** tab and search for `Pipeline Utility Plugin`. Install without restarting.

## Setup the pipeline

- Click on **New Item** and create a new **Pipeline**

- Under Pipeline, choose **Pipeline script from SCM**, and choose **Git** as the SCM.

- Configure the **Repository URL** to point to the current Git repository 

## Test CI and CD process




