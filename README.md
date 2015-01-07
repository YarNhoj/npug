# NPUG: Docker 101

---

# Agenda

##How do I get Docker

##Introductions

##What is Docker

##Docker vs VM's

##Why should I care?

##Demo Time

##Networking in Docker

##More Demos!

##Shoot The Messenger

---

#How do I get Docker

* CentOS/RHEL Docker is in the EPEL

        # yum install -y epel-release
        # yum install -y docker-io

* Ubuntu

        # sudo apt-get install -y docker.io

* Mac/Windows

        # sudo make me a sandwhich and I might tell you

In all seriousness on Mac/Windows you will use boot2docker :)

---

#Introductions



    #finger $speaker
    Login: yarnhoj                   Name: John R. Ray
    Directory: blog.johnray.io       Shell: /usr/bin/consultant
    On since Mon May 5 08:00 (EST) on :Shadow-Soft from :Leidos 
    (messages @theyarnhoj)
    Mail at <jray@shadow-soft.com>.
    Plan to try and take over the world.




    # getent company $speaker
    Shadow-Soft:x:1:1:OSS Integrator and Docker Partner founded in 2008,,,

---

# What is Docker

Containers are built on the idea of Kernel Namespaces.

Namespaces are an abstraction that make it seem like each process has it's own isolated instance of a global resource.

Docker is an platform for developers and sysadmins to build, ship, and run distributed applications in containers

It is a building block for creating distributed systems. 

Containers behave the same regardless of where, when, and alongside what they run.

Docker can run on any x64 machine with a modern linux kernel.

Traditional OS; Ubuntu, CentOS, RHEL

Light OS; TinyCore, CoreOS, Atomic

Hosted; GCE, Amazon, IBM

---

# Containers vs VM's

Containers are NOT virtual machines.

Virtual machines have a full OS with lots of overhead, Containers share the host’s OS

Near native performance because you don't deal with the vitual hardware

The reduction is overall cost also allows greater density on the host

Containers launch near instantly.

Containers aren't going to replace VM's...Yet

---
# Containers vs VM's

## What VM's Do Better

* Running multiple OS's
* Aren't dependent on the Linux Kernel
* More refined Orchestration

## What Containers Do Better

* Faster Boot
* Elastic resource allocation 
* Extremely high density

---

#Why should I care?

Docker creates a standard that many of the big players are quickly adopting. 

IBM, Amazon, Google, and Microsoft have announced hosted versions of their Docker based container solutions.

Red Hat's upcoming Openshift V3 will be based on Kubernetes and Docker

Docker containers give system administrators a new way to allocate compute resources 

Introduces a whole new set of networkng needs

---

#Is it really that big of a deal?

There are over 22 thousand projects on github related to docker.

A quick google search reveals a lot of hits

Docker + Cisco = 500k

Docker + VMWare = 800k

Docker + Amazon = 700k

Docker + IBM = 800K

Docker + Microsoft = 1.3m 

---

#Enough with the words

---

#Building an nginx container

    # mkdir /npug/nginx && cd /npug/nginx
    # vim Dockerfile

##Docker File

    FROM debian:jessie

    RUN apt-get update && apt-get install -y\
        curl\
        nginx-light\
        && apt-get clean

    RUN echo "daemon off;" >> /etc/nginx/nginx.conf

    EXPOSE 80

    CMD ["nginx", "-c", "/etc/nginx/nginx.conf"]

## Build It

    # docker build -t npug/nginx .

## Run Your Container
    
    # docker run -it -d --name web -P npug/nginx
    # docker inspect web
    # curl ${web_ip}

---

#Networking in Docker

---

#Docker0

When Docker starts, it creates a virtual interface named docker0 on the host machine. 

It randomly chooses an address and subnet from the private range defined by RFC 1918 

Virtual Ethernet bridge 

Automatically forwards packets between any other network interfaces that are attached to it. 

Every time Docker creates a container, it creates a pair of “peer” interfaces 

Docker has an extensive guide on all of the networking options including; 

* Building your own bridge
* How to customize docker0 
* configuring DNS

Head over to https://docs.docker.com/articles/networking/ for more information.

---

#The Container Namespace

Using the --net option allows you to declare a container as the namespace for other containers.

This allows a single point of entry into all your containers.

#Presenter Notes
Load up the nginx container with a busybox images as the namespace show that you can curl the port from all containers and the host

---

#Container Networking

Over the years, networking for virtual machines has evolved tremendously

Hypervisors routinely support advanced networking capabilities

Containers are not there...Yet.

A Few Issues:

* Controlling how applications are launched and under what conditions
* The existing networking solutions are either slow, restrictive, or too speciallized for general use
* Security is not all there
* Networking of containers is NEW!!!

---

#Existing Solutions

Networking solutions that are currently being used for containers:

* Docker 
* Pipework
* Kubernetes
* Flannel
* Weave 

---

#Weave

Weave can traverse firewalls and operate in partially connected networks 

Traffic can be encrypted, allowing hosts to be connected across an untrusted network

Weave creates a virtual network that connects Docker containers deployed across multiple hosts

Applications use the network just as if the containers were all plugged into the same network switch

No need to configure port mappings, links, etc. 

---

#Ready Aim Fire
