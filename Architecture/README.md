# SELFNET Architecture

SELFNET intends to provide Self-Organising capabilities over 5G networks by means of an architecture based on six differentiated layers.

![SELFNET ARCHITECTURE](SELFNETframework2017.jpg)

## Infrastructure Layer

This layer provides the resources required for the instantiation of virtual functions (Compute, Network and Storage) and supports the mechanisms for that instantiation. All network functions managed autonomously by the SELFNET framework will be based on this infrastructure. To achieve its functionality, this layer encompasses different sublayers. The Physical sublayer provides physical connectivity, networking, and computation and storage capabilities over bare metal. The Virtualization sublayer provides virtualization capabilities to instantiate virtual infrastructures. Cloud Computing sublayer provides multi-tenancy support to the infrastructure layer together with a centralised point for facilitating the management of the infrastructure.

### Components


## Virtualized Network Layer

This layer represents the instantiation of the Virtual Networking Infrastructures created by the users of the infrastructure as part of their normal operational plan and those created by the SELFNET framework as part of the SON capabilities. In the context of SELFNET, all Network Functions will be virtual functions and they will be chained across the virtual network topology.

### Components

## SON Control Layer

This layer contains the applications that will enable the collection of data from sensors deployed through the entire system (SON Sensors) and the applications that will be responsible for enforcing actions into the Network (SON Actuators) as part of the enabling mechanisms to provide network intelligence in 5G networks.

### Components

* **FlowT** - SDN Application compatible with OpenDaylight controller APIs to apply SON actuation forwarding rules in physical and virtual switches for selective flow mirroring, diversion and drop operations.

## SON Autonomic Layer

This layer provides the mechanisms to provide network intelligence. The layer collects from the network pertinent information about the network behaviour, uses that information to diagnose the network condition, and decides what must be done to accomplish the system goals. It then guarantees the organised enforcement of the actions that are determined.

### Components

* [App Catalogue](https://github.com/Selfnet-5G/app-catalogue) - The SELFNET onboarding service to register and upload individual Apps,  i.e. VNFs, PNFs, SDN-Apps and SDN Controller Apps.

* [AIE](https://github.com/Selfnet-5G/Autonomic-Intelligence-Engine) - Hosts and curates machine learning based elements of the Intelligence in the SELFNET Framework. It is interfacing with the Monitoring-, Aggregation Layers and TAL-Engine. This allows for complex system diagnosis and runtime generation of new symptoms – enabling the SELFNET framework to learn and evolve over time.

* **TAL Engines** - This is a set of two components that are responsible for 
enforcing the onboarded TAL scripts. One engine considered as TAL 
connector is integrated with the Monitoring NBI interface for collecting 
the foreseen by the TAL script alarms and metrics. This engine 
instantiates separate objects per TAL  symptom in the role of 
listeners/filters according to the TAL definitions. It produces symptom 
structures that are forwarded to the main TAL Engine. The main TAL 
engine maintains also different processing objects and spaces for every 
TAL definition and processes the symptoms according to each TAL script. 
For those scripts foreseeing Analyser processing a set of information 
units is propagated to the Analyser and corresponding outputs are 
collected. Either with Analyser involvement or without, the main TAL 
engine applies a rule based lookup and creates Tactics to be forwarded 
and processed by the Action Enforcer. TAL Engines support onboarding of 
TAL scripts, inventory of discovered symptoms and related tactics along 
with the feedback on the status of the deployment, options for pausing 
and restarting a symptom processing as well as resetting of the 
inventory and update or removal of the TAL scripts.


## NFV Orchestration & Management Layer

It is worth emphasising that the control of the chaining of the NF applications is envisioned as a management functionality to be able to control the topology of the Virtual Network layer depicted in the figure as Network Controller (SDN App) and included logically in the VIM functionalities.

### Components

* **App Manager** - This component maintains an abstraction layer that allows 
the Service Orchestrator to handle interactions with underlying 
resources provided as APPs in a uniform way. App Manager defines several 
aspects pertaining to abstraction of applications and how these can be 
specialized during runtime for the proper interaction with the 
application resources for the utilization of the operations that 
actuators and sensor offer. App Manager is integrated with App 
onboarding process for all types of Apps (VNFs, SDN Apps, PNFs). It 
supports the SDN App lifecycle and additionally follows VNF onboarding 
by automating the process of basic NS preparation. With respect to VNFs, 
App Manager maintains a view of the instantiated VNFs and generates for 
every instance an abstraction object to be invoked by Service 
Orchestrator. App Manager is also contacted by Service Inventory for the 
instantiation of the PNF abstraction objects for every PNF entity 
registered. Finally, App Manager maintains an inventory per application 
instance containing all the configurations applied as actuation requests 
in the context of Autonomous Management.

* **SELFNET VNFM** - The NFV Applications lifecycle management service compliant with ETSI NFV MANO principles and specifications.

* **Service Inventory** - The SELFNET inventory function to store and maintain information related to end-to-end services, SDN, NFV and infrastructure resource instances in support of Service Orchestration logics.

* [Topology Manager](https://github.com/Selfnet-5G/topology-manager)  - The Topology Manager provides an updated inventory of both physical and virtual resources available in the infrastructure. It carries out a continuous monitoring of the status of the resources and it is able to report migrations, creations, replacements, deletion and updations of both physical and virtual components. 

* [LTE Topology Manager](https://github.com/Selfnet-5G/lte-topology-manager)  - The LTE Topology Manager provides an updated inventory of all the UEs connection to the LTE antennas of the infrastructures. It carries out a continuous monitoring of the status of the resources and it is able to report UE handovers, connections, reconnections and disconnection events. 

* [Infrastructure Inventory Manager](https://github.com/Selfnet-5G/infrastructure-inventory-manager)  - The Infrastructure Inventory Manager is in change of storing in database the updated status of all the inventory of the resources of hte infrastructure. it includes physical and virtual machines togehter with UEs. It received the information form the LTE Topology Manager and the Topology Manager and stored it in the database keeping a control of the life-cycle of such components. 

## SON Access Layer

This layer encompasses the interface functions that are exposed by the framework. Despite the fact that internal components may have specific interfaces for the particular scope of their functions, these components contribute to a general SON API that exposes all aspects of the autonomic framework, which are “used” by external actors, like Business Support Systems or Operational Support Systems.
A GUI is also provided on top of the SON API where a network administrator can interact and configure SELFNET and also obtain the complete status of the network, acting as a command and control centre. This GUI will also enable the network administrator to stop, verify or manually enforce any of the actions that SELFNET is governing, allowing always network administrators to have control over their infrastructure.

### Components

* [API Broker](https://github.com/Selfnet-5G/NBI) - Acting as the SELFNET's Northbound interface the API broker collects information from other SELFNET components
* [GUI](https://github.com/Selfnet-5G/GUI) - SELFNET's component that present a visual representation of SELFNET's status

## Use Cases

SELFNET's architecture and Self-Organizing capabilities are demonstrated through three different [use cases](../Use%20Cases).

