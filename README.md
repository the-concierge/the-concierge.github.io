# The Concierge

> Simple continuous integration and a bit of Docker orchestration with Node

## What is it
The Concierge is a self-contained application that provides a front-end for Docker. It allows to create, manage and inspect your containers and images.  
In addition, it allows you to create **Applications** which are Git repositories. The Concierge will monitor these repositories and automatically build images.

### A bit of history
The Concierge was first created in Febuary 2015 as a private project to solve a business problem. It was originally intended to build our internal application and deploy it. The purpose was for managing different feature sets of the same application and managing which client was on what 'flavour' (feature set) of the application. It would also manage upgrades and rollbacks for groups of clients.

Since then, we realised it had a lot of general usefulness. The business specific logic has been removed and it has been open sourced. It has changed direction and become a general purpose continuous integration tool for developers. It has since gone through several refactors and is still a work in progress, but is already usable in its current state.

## Getting Started
See the [Quick Start guide](guide) for getting started

## Contributing
The Concierge is open to contributors and feedback. Please feel free to [submit ideas and feedback](https://github.com/the-concierge/concierge/issues) and [contribute](https://github.com/the-concierge/concierge/issues?q=is%3Aissue+is%3Aopen+label%3Aapproved)!

The Concierge is an evolving application. I am constantly improving existing features and adding new features. The GitHub issue tracker is the best place to see what is in the pipeline.

## Features

### Containers
- Run and manage containers
- Logs and Performance monitoring over time
  - The Concierge will record CPU and memory usage and display this information is easy to read graphs
  - View container logs 
- Real-time container monitoring
  - View the CPU and memory usage of containers in real-time from the Containers dashboard
  - ~~Monitor container logs~~ _TODO_
- Provides reverse proxying to create vanity URLs for containers
  - _Requires configuration_

### Images
- Run instances of images
- Easily toggle which ports to expose
- Optionally provide custom ports to expose on the Host
- Easily edit environment variables and provide additional custom variables
- Create links to existing containers
  - Concierge will use **Container Networking** instead of **Linking** in the near future
- Easily create volumes and provide additional custom volumes

### Applications
- Automatically build images on Git Push
- Manually build images from branches or tags
- Real-time overview of branch status (waiting, building, success, failed...)
- Run containers from successfully built branches