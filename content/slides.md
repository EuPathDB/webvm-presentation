**EuPathDB Website VM Appliances**

December 2014



## Background

  - EuPathDB hosts websites accessible over the public internet.
  - Hosted on physical servers in data centers in Athens, Philadelphia.
  - Operating system, Apache webserver, Tomcat application server, Oracle databases

Note:
We host public websites on server hardware in datacenters in Athens, Philadelphia.
Websites are backed by two Oracle databases, also hosted in our datacenter.
We can also package a website and databases on to a virtual machine that includes
everything



  - We can also bundle everything into a single, standalone virtual machine



## Why VMs?

  - Carry to conferences, workshops where internet connectivity is poor
  - Archive previous releases
  - _Host at institutions where internet connectivity is poor._



## SIG Goals

  - Give overview of the labor costs of generating VMs
  - Discuss how to reduce those costs
  - Highlight concerns: security, user support, legal



## Questions

  - Why does it take a week to make a VM?
  - Can it be done in less time?
  - Why isn't the process automated?
  - This VM is broken. Why didn't you test it better?



## Creating A VM



## Leveraged Technologies 

<span style="color:blue; font-size:75%">( 0-5 maturity)[+ core infra, - saVM specific]</span>

  - KVM                                         <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(3.5)[+]</span>
  - dedicated laptop and custom UI              <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(3)[-]</span>
  - Puppet                                      <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(3.5)[+]</span>
  - self-configuring Apache hosts               <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - Tomcat Instance Manager                     <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
    - <span class='small-bullet-link'>[https://github.com/EuPathDB/tomcat-instance-framework](https://github.com/EuPathDB/tomcat-instance-framework)</span>
  - GUS build <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - rebuilder <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - configula - automated WDK configuration <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(3)[+]</span>
  - /dashboard <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>

Note:
- VMs are mostly an extension of core infrastructure - just another server
- have to take care of core infra before tackling VMs
- most of the technology is in place for pipelining VM generation



## VM Contruction Overview



VM Contruction Overview

## Create VM template

  - Kickstart bootstrap
  - Puppet deployment of core software, configuration
  - manual QA, tweaks



VM Contruction Overview

## New VM from Template

  - update OS patches
  - update from latest Puppet manifests
  - configure network
  - resize disks



VM Contruction Overview

## Clone Databases

  - export production database to a file
  - on VM: NFS mount the production export directory
  - create database
  - import the export file
  - repeat for apicomm


VM Contruction Overview

## Install Website

  - checkout source code
  - build



VM Contruction Overview

## Install webService files
  
  - 400 GB
  - exclude BAM files
  - 15 GB



VM Contruction Overview

## Run tuningManager

  - additional software install
  - additional configuration
  - additional complexity
  - additional point of failure
  - additional time



## QA the website



## Pitfalls of manual assembly

  - labor intensive
  - disruptive to other project tasks
  - long lead time required
  - 3-6 months between assemblies
    - what is now broken, out of date?



## Pipeline the process



## Offprint

  - https://github.com/EuPathDB/offprint
  - `offprint w1.toxodb.org`
  - /dashboard API
    - source code versions
    - databases to clone
    - WDK configuration
  - import directly from live production DB
    - no tuningManager



## Distribution Issues
(Group Discussion)


Issues:

## Remote Support

  How do we provide it?

  - too complex for novices
  - remote access, past firewall/NAT
  - end-user changes complicate support
  - OS security updates



Issues:

## Licensed Software

  - Oracle
  - Java Development Kit
  - WU-BLAST (deprecated)
  - _signalp_
  - _tmhmm_
  - others???

Note: 
  - Redistribution of Runtime Environment is OK. Redistribution of JDK has some restrictions.
    - need JDK to compile WDK in situ
  - wublast now replaced with Public Domain NCBI blast
  - signalp, tmhmm currently not included on VMs, but need to be aware that it does not creep in



Issues:

## Security

  - Oracle user accounts include passwords
  - apicomm has user search history, contact info and passwords
  - leakage of sensitive system details
    - deployed by Puppet, user shell history after setup

Note:
how to clone only data:
need careful refactoring of Puppet manifests
need dedicated user account for build on removable disk



### Needed Infrastructure Improvements
(Group Discussion)



Needed Infrastructure Improvements:

## API for schema requirements

  What are the minimum schema/tables required?

  - avoid private user schemas
  - keep up with application changes through releases
  - e.g. GUS `core.info`
    - core.info does not include tuning tables
    - apicomm has no equivalent



Needed Infrastructure Improvements:

### Remove user data from apicomm

  - Make empty apicomm on the VM?
    - loss of example strategies
    - loss of community uploaded files
    - are apicomm schema installation scripts up to date?
  - Clone subset of production apicomm, excluding community profile data?



Needed Infrastructure Improvements:

## Lock tuning tables

  Live import fails when tuningManger is running

  - block tM when exporting
  - block export when tuning



Needed Infrastructure Improvements:

## Automated QA




## Future
  - full pipeline build
  - Jenkins integration builds
  - migrate from VMWare to VirtualBox
  - snapshot all sites every release?
