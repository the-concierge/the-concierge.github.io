# Quick Start

Pre-requisites:
- Docker CE is installed locally

## Installation

### Using NPM
The easiest way to get started is to install the Concierge via [NPM](https://nodejs.org):
```bash
> npm install the-concierge -g
> the-concierge start
> [11:01:36] INFO: Successfully executed 'start'
> [11:05:28] INFO: The Concierge is running on http://localhost:3141
```

The Concierge URL will be available on the command line. Open up your browser and head to that URL.

### Using Docker
Alternatively, you can also run Concierge in Docker, but it will need access to your Docker socket:
```bash
docker run -dt --restart=always -p 3141:3141 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -name concierge \
  theconcierge/concierge:latest
```

### Using Source
```bash
> git clone https://github.com/the-concierge/concierge
> cd concierge
> yarn
> yarn build
> yarn start # using PM2
> node . # using Node directly
```

## Creating a Host

_The Concierge currently only supports managing a single, local, Docker daemon. The Concierge will manage multiple hosts in the future._

To get started, you will need to have a **Host** configured. The easiest way to get started to manage your local Docker daemon:
- Go to the Hosts tab
- Click **Create Host**
- Click **Save**

Once we have a **Host** set up correctly, we can now see our Containers and Images

## Your First Application
Using public Git repositories is the simplest way to demonstrate how the Concierge works. Applications **must** have:
- a **Dockerfile** in the root directory
- or you must provide the location in the repository to the **Dockerfile** you wish to use

As an example, you can use an existing repository that I use for testing:
- Go to the **Applications** tab
- Click **Create**
- Choose a **Name**
- In the **Repository** field enter: `https://github.com/aethant/vanilla-css`
- Click **Save**

The Concierge will now begin tracking the repository. 
- Click **Build** next to your new Application
- Choose the branch `gh-pages`
- Click **Deploy**

And you're done! The Concierge will now pull down the code and create and Docker image. You'll be able to run this image once it is done.

## Automatically Pushing to a Docker Registry
See [Concierge Configuration](guide?id=concierge-configuration)

## Working with Private Repositories
The Concierge allows you to create re-usable credentials. These can be username/password combinations or private keys. You can create these from the  **Credentials** tab.

When creating or editing an **Application**, you can choose the **Credentials** the application should use from the Credentials dropdown menu.

## Concierge Configuration
_The Concierge has very little configuration at present. It is currently fairly opinionated, but that is changing_

### Docker Registry
If a valid **Registry** is configured, it will automatically push built images to this registry.  
The registry must be provided as **HOSTNAME**:**PORT**. E.g. localhost:5000

### Proxy Hostname
The Concierge provides a reverse proxy service to running Containers. Providing a **Proxy Hostname** will enable this feature. All requests to **CONTAINER NAME**-**INTERNAL CONTAINER PORT**.**PROXY HOSTNAME**:**CONCIERGE PORT** will be reverse proxied to the container.

E.g.:
- Setting a **Proxy Hostname** of `docker.local.dev` 
- Creating a container named `web`
- With an exposed _internal_ port of 3000

Will create a vanity URL of: `web-3000.docker.local.dev:3141`

It is up to you to ensure `*.docker.local.dev` requests are routed to the Concierge. This can be achived using a tool like **DNSMASQ**.

### Statistics
The Concierge is constantly monitoring all containers CPU and memory usage at a fix rate of 1 sample per second (1Hz). You can configure how much data is kept (`Retention days`) and how many samples are used to populate a "Bin" (`Samples per bin`).

Bin: A bin is a set of samples over a time period. This is used to calculate the "box" (min, max, quartiles, median) stats for a time period. Setting `Samples/Bin` to `300` would collect 5 minutes of data for a bin.