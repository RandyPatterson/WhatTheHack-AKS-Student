# Challenge 01 - Path A: Got Containers?

[< Previous Challenge](./Challenge-01.md) - **[Home](../README.md)** - [Next Challenge >](./Challenge-02A.md)

## Introduction

The first step in our journey will be to take our application and package it as a container image using Docker.

## Description

To help ensure everyone can start this hack on the same page and avoid the complexities of installing and setting up Docker, we have provided you with an Lab VM with Docker & Node.js tools pre-installed.

You will use this VM during this challenge to perform several tasks to prepare the application for containerization and eventual deployment into Kubernetes, including:
- Build and run the Node.js-based FabMedical application locally on the VM to observe how it works
- Create a set of Dockerfiles to build container images of the application
- Run the containerized application on the VM to observe how it works in the Docker environment


### Build & Run the FabMedical Application

From the PowerShell Terminal on the Lab VM, navigate to the FabMedical application folder and run the application to see how it works.

```PowerShell
cd \WhatTheHack-AKS-Student\Student\Resorces\Challange-01
```


- Run the Node.js application
	- Each part of the app (api and web) runs independently.
	- Build the API app by navigating to the `/content-api` folder and run `npm install`.
	- To start the app, run `node ./server.js`
	- Verify the API app runs by hitting its URL with one of the three function names. Eg: **<http://localhost:3001/speakers>**
- Open another Powershell terminal and repeat the steps above for the content-web app which is located in the `/content-web` folder, but verify it's available via a browser on the Internet!
	- **NOTE:** The content-web app expects an environment variable named `CONTENT_API_URL` that points to the API app's URL. 

	In PowerShell set the environment variable using the following command
	```PowerShell
	$Env:CONTENT_API_URL = "http://localhost:3001"
	```

### Create Dockerfiles to Containerize the FabMedical Application

- Create a Dockerfile for the content-api app that will:
	- Create a container based on the **node:8** container image
	- Build the Node application like you did above (Hint: npm install)
	- Exposes the needed port
	- Starts the node application

- Create a Dockerfile for the content-web app that will:
	- Do the same as the Dockerfile for the content-api
	- Also sets the environment variable value as above

- Build Docker images for both content-api and content-web

### Run the Containerized FabMedical Application with Docker

- Run both containers you just built and verify that it is working. 
	- **Hint:** Run the containers in 'detached' mode so that they run in the background.
	- **NOTE:** The containers need to run in the same network to talk to each other. 
		- Create a Docker network named "fabmedical"
		- Run each container using the "fabmedical" network
		- **Hint:** Each container you run needs to have a "name" on the fabmedical network and this is how you access it from other containers on that network.
		- **Hint:** You can run your containers in "detached" mode so that the running container does NOT block your command prompt.


## Success Criteria

1. Verify that you can run both the Node.js based web and api parts of the FabMedical app on the VM
2. Verify that you have created 2 Dockerfiles files and created a container image for both web and api.
3. Verify that you can run the application using containers.

## Learning Resources

- [Dockerizing a Node.js web app](https://nodejs.org/en/docs/guides/nodejs-docker-webapp/)
- [How to Dockerize a Node.js application](https://buddy.works/guides/how-dockerize-node-application)
- [Why and How To Containerize Modern Node.js Applications](https://www.cuelogic.com/blog/why-and-how-to-containerize-modern-nodejs-applications)


After your Coach verifies your success criteria continue to [Challenge 02A](./Challenge-02A.md)