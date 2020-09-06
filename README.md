
# Openshift

## Introduction

Openshift is Red Hat open source container application. 

Openshift Origin is based on top of Docker containers and Kubernets cluster manager,with added developer and operation centric Tools that enable rapid application development, deployment and lifecycle management.

[     Tools     ]
[   Kubernetes  ]
[     Docker    ]

Tools like SCM, pipelines (develop, build and deploy), Registry, Software defined networking, API centric and Governance.

## Architectural overview



### Components

- Kubernetes
- Containers
- Images

## Setup - Minishift

1. Download minishift release for our operating system.
2. Copy the contents of the directory to your preferred location.

     cp minishift ~/bin/minishift

3. Add ~/bin folder to our path environment variable.

     export PATH=~/bin:$PATH


4. Start minishift

     $ minishift start

user: system
password: admin

## Management - Web, CLI, API


     > oc login -u system -p admin

     > oc logout


### Access with API

     > curl https://localhost:8443/opai/v1/users \
        -H "Authorization: Bearer <Token>"
     
    # returns our bearer token
     oc whoami -t 