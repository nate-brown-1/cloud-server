# Lab 16: AWS: Cloud Servers

## Overview

Deploy a Node.js server to AWS EC2

## Resources

### Feature Tasks

Deploy a simple Node.js server to EC2, using Elastic Beanstalk

Choose a server you’ve built previously

Option 1: A simple API or Web Server

Option 2: A socket.io event Hub

The server should not require a database

Check in your server to GitHub

### Task 1

Create a new environment, using Elastic Beanstalk from the AWS Control Panel (GUI)

Manually deploy your application to this environment by uploading a .zip file

### Task 2

Using the same server, create a new environment using Elastic Beanstalk from your terminal

Manually deploy your application to this environment by using eb deploy

### Documentation

In your README.md include:

The links to both of your deployed servers (GUI deploy and CLI deploy)

Document your processes

### Stretch Goal

Automatically deploy your app to either (or both) environments on check-ins to your main branch using a github action

HINT: Explore the GitHub marketplace

### Submission Instructions

Create a new repository for your server, called ‘cloud-server’

Work on a non-main branch and make commits appropriately.

Update your README.md file with the required documentation above.

Create a pull request to your master branch with your work for this lab.

Submit the link to that pull request on Canvas.

### Process Documentation

Task 1: Use EB GUI

- Set up S3 bucket: change permissions to use ACLs because app won't build with ACLs disabled (default)
_ Zip the repo: must zip the individual files together, can't zip the parent directory
- Upload the zip file in EB console, Node 18, build
- Deployment succeeds with health warning: all requests failing with code 5xx
- Rebuild the deployment a bunch of times in the CLI, see below
- Get CLI deployment to work in Node 16
- Zip it and build a new application and environment using the GUI

GUI Deployment link

[http://nates-basic-express-server-env.eba-wgxf6yvs.us-west-2.elasticbeanstalk.com/](http://nates-basic-express-server-env.eba-wgxf6yvs.us-west-2.elasticbeanstalk.com/)

NOTE: This deployment gets "severe" health rating with 100% of the HTTP requests failing

Task 2: Use EB CLI

- Set up user "cli-user"
  - Download user credentials (password) as CSV file
  - Download user access keys as CSV file
- Run "eb init" to setup environment defaults for build
- Have the build fail at least 20 times
- Figure out that Amazon Linux 2 instance is using a version of glibc that was incompatible with the version of Node.js that I built the apps with
- Figure out that this is a known issue and Amazon Linux 2022/2023 is supposed to correct it, but isn't available to me
- Install nvm and multiple versions of Node.js
- Figure out that EB is not compatible with Node 16.20.0 (the last release of Node 16 and the LTS version)
- Successfully build the site with Node 16.19.1
- Profit?

CLI Deployment Link

[http://cli-nates-basic-express-server-dev.us-west-2.elasticbeanstalk.com/](http://cli-nates-basic-express-server-dev.us-west-2.elasticbeanstalk.com/)