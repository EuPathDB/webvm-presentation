**EuPathDB Website VM Appliances**

December 2014



## Goal

  - All development, architecture made with VM in mind
    - Recent SIG on authentication ... authN service ... how will that be supported on VMs without network



## What is a virtual machine



## Leveraged Technologies 

<span style="color:blue; font-size:75%">( 0-5 maturity)[+ core infra, - VM specific]</span>

  - KVM <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(3.5)[-]</span>
  - VMware <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(4)[-]</span>
  - dedicated laptop and custom UI for VMs <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">defunct (3)[-]</span>
  - Puppet <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(3.5)[+]</span>
  - standardized directory naming conventions <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - self-configuring Apache hosts <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - scripted website framework installation <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - Tomcat Instance Manager <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>

Note: 
Puppet low maturity because it needs refinement to ensure minimal installation (no leakage of sensitive internals)



## Leveraged Technologies  <!-- .class="highlight-red" -->

  - GUS build <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - rebuilder <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - configula - automated WDK configuration <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(3)[+]</span>
  - /dashboard <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(5)[+]</span>
  - Oracle network import, our implementation <!-- .element: class="fragment" --> <span style="color:blue; font-size:75%">(2)[-/+]</span>

Note:
- VMs are mostly an extension of core infrastructure - just another server
- have to take care of core infra before tackling VMs
