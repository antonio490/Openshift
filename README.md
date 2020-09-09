
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
     Starting local OpenShift cluster using 'kvm' hypervisor...
     ...
     OpenShift server started.
     The server is accessible via web console at:
     https://192.168.99.128:8443

     You are logged in as:
     User:     developer
     Password: developer

     To login to your Minishift installation as administrator:
     oc login -u system:admin



## Management - Web, CLI, API


     > oc login -u system:admin

     > oc logout


### Access with API

     > curl https://localhost:8443/opai/v1/users \
        -H "Authorization: Bearer <Token>"
     
    # returns our bearer token
     > oc whoami -t 

## Projects and Users

Openshift can hold hundreds of projects in form of pods. In order to
help teams to manage applications, openshift has projects. Namespaces provide isolation.

There are three types of users: Regular user (developer), system user (cluster admin system:admin and system:master) and service user (system:serviceaccount).

By default minishift comes with an allow all policy authorization. In case of an advanced installation Deny all policy is also used. Configuration is provided under this file: /etc/openshift/master/master-config.yaml

<code>

    $ oc login -u system:admin

    > oc get projects

    > oc get users

    > oc adm policy add-cluster-role-to-user cluster-admin administrator

</code>

## Builds and deployment

Openshift creates builds referencing source code management repositories (Github, Bitbucket or Gitlab). It downloads the source, build an image, push it to Registry and Deploy the application on the build in kubernetes cluster. Everything is taking care by openshift and it only requires us to provide the source repository url.

### Build triggers

Instead of launching builds manually it is more convenient to do it automatically, in a continious integrated way.

We just need to find on the configuration app screen the webhook URL for our source repository and paste it on the webhook URL payload at the repository settings page.

Source repo --> Webhook --> Openshift

### Deployment


|-----------|--------|------------------------|-----------------------|
| Container |  POD   | Replication Controller | Deployment Controller |
|-----------|--------|------------------------|-----------------------|

How often does a deplyment update?

- We can manually trigger the update or configured to automatically update everytime a job build runs.
- Easy and flexible.
- Rolling strategy means that every replica is also update.