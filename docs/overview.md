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


## Ok... but why not start this project from scratch?

This is a valid question because on some level, building out the entire system would likely give me a unique set of skills, and maybe I would make different choices and, and, and… there are a million reasons why I should build this from scratch. But I have a few reasons why I am choosing to build on top of the Huly platform.
What it comes down to is really a few things.
I mean for one, my goal is not to build a productivity platform alone.
But also, I believe that this approach is more likely to give me the experience I am looking for, working within more defined boundaries and working with a codebase that existed long before I was involved.



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
To modify the database, we will need to make changes to the `platform/models` directory. 
```bash
/platform$ tree models 
models
├── activity
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── actions.ts
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   ├── notification.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── all
│   ├── CHANGELOG.json
│   ├── CHANGELOG.md
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   └── migration.ts
│   └── tsconfig.json
├── attachment
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── bitrix
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── board
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── calendar
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── chunter
│   ├── CHANGELOG.json
│   ├── CHANGELOG.md
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── contact
│   ├── CHANGELOG.json
│   ├── CHANGELOG.md
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── controlled-documents
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   ├── permissions.ts
│   │   ├── plugin.ts
│   │   ├── roles.ts
│   │   ├── spaceType.ts
│   │   └── types.ts
│   └── tsconfig.json
├── core
│   ├── CHANGELOG.json
│   ├── CHANGELOG.md
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── benchmark.ts
│   │   ├── component.ts
│   │   ├── core.ts
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   ├── permissions.ts
│   │   ├── security.ts
│   │   ├── spaceType.ts
│   │   ├── status.ts
│   │   ├── transient.ts
│   │   └── tx.ts
│   └── tsconfig.json
├── document
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── drive
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── gmail
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── guest
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   ├── plugin.ts
│   │   └── utils.ts
│   └── tsconfig.json
├── hr
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── inventory
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── lead
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   ├── plugin.ts
│   │   ├── spaceType.ts
│   │   └── types.ts
│   └── tsconfig.json
├── love
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── notification
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── preference
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   └── migration.ts
│   └── tsconfig.json
├── presentation
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── print
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── products
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   ├── plugin.ts
│   │   └── roles.ts
│   └── tsconfig.json
├── questions
│   ├── config
│   │   └── rig.json
│   ├── jest.config.js
│   ├── package.json
│   ├── src
│   │   ├── doc-types
│   │   │   ├── base.ts
│   │   │   ├── index.ts
│   │   │   ├── mixin.ts
│   │   │   └── questions
│   │   │       ├── MultipleChoice.ts
│   │   │       ├── Ordering.ts
│   │   │       └── SingleChoice.ts
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── recruit
│   ├── CHANGELOG.json
│   ├── CHANGELOG.md
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   ├── plugin.ts
│   │   ├── review.ts
│   │   ├── spaceType.ts
│   │   └── types.ts
│   └── tsconfig.json
├── request
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── server-activity
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   └── migration.ts
│   └── tsconfig.json
├── server-attachment
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-calendar
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-chunter
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-collaboration
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-contact
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-controlled-documents
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-core
│   ├── CHANGELOG.json
│   ├── CHANGELOG.md
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-document
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-drive
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-gmail
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-guest
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-hr
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-inventory
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-lead
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-love
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-notification
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-openai
│   ├── CHANGELOG.json
│   ├── CHANGELOG.md
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-products
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-recruit
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-request
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-setting
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-tags
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-task
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-telegram
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-templates
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-time
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-tracker
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-training
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-translate
│   ├── CHANGELOG.json
│   ├── CHANGELOG.md
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── server-view
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── setting
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── support
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   └── index.ts
│   └── tsconfig.json
├── tags
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── task
│   ├── CHANGELOG.json
│   ├── CHANGELOG.md
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── telegram
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── templates
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── text-editor
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── time
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   └── plugin.ts
│   └── tsconfig.json
├── tracker
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── actions.ts
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   ├── plugin.ts
│   │   ├── presenters.ts
│   │   ├── types.ts
│   │   └── viewlets.ts
│   └── tsconfig.json
├── training
│   ├── config
│   │   └── rig.json
│   ├── jest.config.js
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   ├── plugin.ts
│   │   ├── roles.ts
│   │   └── types.ts
│   └── tsconfig.json
├── view
│   ├── CHANGELOG.json
│   ├── CHANGELOG.md
│   ├── config
│   │   └── rig.json
│   ├── package.json
│   ├── src
│   │   ├── index.ts
│   │   ├── migration.ts
│   │   ├── plugin.ts
│   │   └── utils.ts
│   └── tsconfig.json
└── workbench
    ├── CHANGELOG.json
    ├── CHANGELOG.md
    ├── config
    │   └── rig.json
    ├── package.json
    ├── src
    │   ├── index.ts
    │   └── plugin.ts
    └── tsconfig.json

209 directories, 404 files
```

This is where the database models are defined. We will need to create new models for the new tables we want to create, and we will need to modify the existing models to add new fields when necessary.
It is important to me that when it comes to the database, entities are declared once, and referenced where needed using relationships. This way, a task on the to do list is equivalent to the task on, say an AI agents task queue. The display via the UI may be different. There may be fields we add to the database that we do not necessarily put on the web UI

Once you add a new model to the directory, you will need to add it to the `platform/models/all`
```bash
user@cracked:~/platform-1/platform$ tree models/all
models/all
├── CHANGELOG.json
├── CHANGELOG.md
├── config
│   └── rig.json
├── package.json
├── src
│   ├── index.ts
│   └── migration.ts
└── tsconfig.json

2 directories, 7 files
```



### Networking Practices

Generally speaking, we do not want to expose our operations to the internet at large.
That is why it is heavily advised that you do not expose your dashboard UI to the internet, whether it be with a tunnel like Cloudflared, or port forwarding or something. Generally speaking the assumption is that you want to obfuscate the fact that you are using this offensive Huly platform, on top of the fact that it’s just best practices not to expose services unnecessarily 

That being said:
- we still have to access the UI somehow
- Our network scanning systems still have to be able to reach said network to scan
- Our AI/ML systems still have to be able to reach the internet to download models, and preform searches.
- Basically, we need to be exposed sometimes, but we want to do it "right"

#### UI Access
I have a few ideas on how to access the UI:
- HeadScale / Tailscale: This is a VPN service that is designed to be easy to use and set up. It is designed to be self hosted
- Tor Hidden Service: Need to do more research, and testing to see how well this works. This is less than ideal, so will be optional at most

#### Network Scanning
- OpenVPN Profiles + Chained Connections: This is a method of chaining VPN connections together to make it harder to trace back to the source. This is a bit more advanced, and will require some testing to see how well it works
- Torsocks + Proxychains: This is a method of chaining connections together using the Tor network. This would work by passing proxychains configs to the network scanning container, and then using torsocks to route the traffic through the tor network, then out of an "exit proxy" so that you do not have a low rating.
- Rotating API Keys: This is a method of rotating API keys to avoid rate limiting. This is done by providing multiple of the same type of credential to the network scanning container, and then rotating through them as needed.

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



