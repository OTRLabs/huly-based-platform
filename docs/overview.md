# Offensive Huly: Building a Red Team’s “everything app”

## Introduction:

### What is Huly?

[Huly](https://huly.io/) is an *open source project* as well as a `cloud platform` developed by [Hardcore Engineering](https://hardcoreeng.com/)!

It is designed to be a sort of “everything app” primarily for developers. It is a full stack JavaScript application that is designed to be self-hosted, and is built on top of the Svelte front end framework and the Express.js backend framework.

It appears to be highly extensible, offering several existing integrations:
These integrations include:
- GitHub 2 way sync
- Telegram
- Gmail
- Google Drive 


### Why Huly?
The main appeal of using Huly as the foundation for this `red team environment` is that it comes with all of the *collaboration* and `development` features I would want to have in this type of platform. There is no need for me to retread old ground and make the same discord/slack style messaging application, or spend a day stringing together some S3 style service when the team at Hardcore Engineering has already done it for me and done it in a way that makes it easy to extend.

### Ok, but why an "Everything App"?
As it stands, open source "offensive tooling" tends to be very fragmented. There are a lot of tools out there, but they are all separate and don’t really work together. This is not always the case. There are some amazing tools like [Faraday by InfoByte](https://github.com/infobyte/faraday) that make use of a wide variety of community tools. But in general, if you want to combine the output of a network scanner with the output of a web application scanner, you are going to have to do a lot of manual work to get that data into a format that you can use.

On top of that, there is a lot of manual work that goes into setting up and managing a red team environment. You have to set up your C2 server, your phishing server, your payload generation server, your reporting server, your knowledge base, your network scanner, your web application scanner, your host management system, your task management system, your chat system, and so on. This is a lot of work, and it is work that is not always done well. There are a lot of red teams out there that are using a combination of Google Docs, Slack, Discord, and a bunch of other tools to try and manage all of this stuff, and it is not always working out well for them.

TL;DR: I want to build a platform that makes it easy to manage all of the tools and data that a red team needs to do their job, and I want to build it on top of the Huly platform because it is already a great platform that is designed to be extensible.

### My thoughts on Huly

**pros**

- Built in task management
- Self host-able
- built in storage
- 2 way sync with GitHub

**cons**:

- [No built in message encryption.](https://x.com/huly_io/status/1802734334132060528)
- This is more of an opinion, but being full stack JavaScript is a bit of a con for me. I am not a huge fan of JavaScript for a backend language, but they make up for it by using Svelte for the front end.


## Development Plan / Guide:

### 1. Modifying the Huly Platform UI
### 2. modifying the database
It is important to me that we make every effort to use the existing Huly Database. This is because I want to make sure that we are not creating a situation where we have to maintain two separate databases. This is a recipe for disaster. So, we will make every effort to use the existing Huly database, and only create new tables when absolutely necessary.


## Goals:

My plan is to create an environment that can act as a sort of “everything app” for a red team. The idea is to build on top of the existing Huly platform to create additional tools and integrations that are useful for red teaming.

The idea is that we will develop a series of integrations that will allow us to interact with the Huly platform in a way that is useful for red teaming. This will include things like:
- Network Recon Tools
- Centralized Knowledge Base
- Threat Intelligence Feed
- Automated Reporting
- Machine & Host Management
- Attack surface management
- Automated phishing campaigns?
- Automated C2 server deployment
- Automated payload generation?
- Ollama / Hugging Face integration?

These integrations will be designed using a microservice architecture, and will be deployed as docker containers on the same machine you are running the Huly Platform on.
They will communicate via HTTP and will be designed to act as API servers, meaning that they accept a request and return a response in JSON format.

We will primarily write these services using:

## Python
We will use Python for AI/ML focused plugins
- [Litestar](https://litestar.io/)
- [Hugging Face Models](https://huggingface.co/)

## Go
We will use Go for network focused plugins. This includes, network recon, and deployment management stuff. Generally, what `Go` is good for.
- [Gin](https://gin-gonic.com/)

### Network Discovery 
The `network discovery` integration service will be designed to be a Debian based container, that runs sub-containers which are responsible for running the actual network discovery tools. The vast majority of these tools will be written in Go. This is because we will be using a massive amount of our tooling from [Project Discovery](https://projectdiscovery.io/), and they are all written in Go. 

Some examples of tools we want to use are:
- [Nuclei](https://github.com/projectdiscovery/nuclei)
- [Katana](https://github.com/projectdiscovery/katana)
- [Subfinder](https://github.com/projectdiscovery/subfinder)
- [MapCIDR](https://github.com/projectdiscovery/mapcidr)
- [CDNCheck](https://github.com/projectdiscovery/cdncheck)
- [CVEMap](https://github.com/projectdiscovery/cvemap)
- [HTTPX](https://github.com/projectdiscovery/httpx)
- [AlterX](https://github.com/projectdiscovery/alterx)
Some non-project discovery tools we want to use are:
- [Rustscan](https://github.com/RustScan/RustScan)

The network discovery service will be responsible for:
- Running network scans
- Running web application scans
- processing results (using AI/ML) (this will probably be a plugin of its own)
- storing results in the Huly platform to view later


### Centralized Knowledge Base