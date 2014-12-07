**EuPathDB Website VM Appliances**

December 2014



## Goal

  - All development, architecture made with VM in mind
    - Recent SIG on authentication ... authN service ... how will that be supported on VMs without network



## What is a virtual machine



## Leveraged Technologies 

<span style="color:blue; font-size:75%">( 0-5 maturity)[+ core infra, - VM specific]</span>

  - KVM                                         <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(3.5)[-]</span>
  - dedicated laptop and custom UI              <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(3)[-]</span>
  - VMware                                      <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(4)[-]</span>
  - Puppet                                      <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(3.5)[+]</span>
  - standardized directory naming conventions   <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - self-configuring Apache hosts               <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - Tomcat Instance Manager                     <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
    - <span class='small-bullet-link'>[https://github.com/EuPathDB/tomcat-instance-framework](https://github.com/EuPathDB/tomcat-instance-framework)</span>
<!-- - scripted website framework installation   -->

Note: 
Puppet low maturity because it needs refinement to ensure minimal installation (no leakage of sensitive internals)



## Leveraged Technologies

  - GUS build <span style="color:blue; font-size:75%">(5)[+]</span>
  - rebuilder <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - configula - automated WDK configuration <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(3)[+]</span>
  - /dashboard <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - Oracle network import <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(2)[-/+]</span>

Note:
- VMs are mostly an extension of core infrastructure - just another server
- have to take care of core infra before tackling VMs
- most of the technology is in place for pipelining VM generation



Issues:

## Issues: Remote Support

  - too complex for novices
  - remote access, past firewall/NAT
  - end-user alterations



Issues:

## Distributing Licensed Software

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

  - Oracle user accounts w/ passwords
    - should only clone data tables
      - how?
  - leakage of sensitive system details
    - deployed by Puppet, user shell history after setup
      - careful refactoring of Puppet manifests
      - dedicated user account for build on removable disk



Needed Infrastructure Improvements:

## API to schema requirements

  - avoid private user schemas
  - keep up with application changes through releases
  - e.g. GUS core.info
    - core.info does not include tuning tables
    - apicomm has no equivalent



Needed Infrastructure Improvements:

## Lock tuning tables

  - block tM when exporting, block export when tuning



Needed Infrastructure Improvements:

## Automated QA




## Future
  - full pipeline build
  - Jenkins integration builds
  - migrate from VMWare to VirtualBox
  - snapshot all sites every release?


