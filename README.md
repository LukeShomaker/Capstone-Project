# Capstone-Project


This README encompasses Luke and Ajay's Senior capstone Cyber project!!


The overall goal of this project was to implement a working SOC and SOAR

What is a SOC?
SOC stands for Security Operation Center.

To create a SOC, one must implement multiple differnet pieces of software and integrate them  together in order to properly create the SOC

What is a SOAR:
SOAR stands for Security Orchestration, Automation, and Response. It refers to a class of tools that help security teams streamline and enhance their processes by combining orchestration, automation, and incident response capabilities.

Hardware Requirements:
500GB storage (Preferably 1TB)
32GB Ram

ISO images Needed:
Proxmox ISO image
OPNsense ISO image
Ubuntu version 20.04 or newer (gui or server, gui was the primary ISO image used)
Windows11 ISO image

SOC Software:

OPNsense/Surricata:
OPNsense is a software that can be used as a router for this setup. 
Surricata is the default IDS that is installed on OPNsense.

Wazuh Stack:
This stack manages the visualization software to see reports based on malicious traffic on the network.
A wazuh agent needs to be install on the OPNsense router to allow integration with the manager.
A wazuh agent is needed on endpoints that you want to collect data from.
The wazuh indexer deals with data manipulation.


SOAR Software:
TheHive:
  TheHive is an incident response platform (IRP) designed to help security teams manage and respond to cybersecurity incidents. Here are some of its features: 
    Case Management: Organizes incidents into cases, which can be assigned to team members.
    Collaboration: Allows team members to collaborate and share findings in real time.
    Automation: Integrates with Cortex for automated analysis and task execution.
    Alert Ingestion: Imports alerts from various sources (e.g., SIEMs, MISP) to create cases for investigation.
Customization: Offers customizable workflows and templates to adapt to specific team needs.
Misp:
  MISP is a threat intelligence platform (TIP) that facilitates the sharing, storage, and analysis of threat data. Heres its features: 
    Threat Data Sharing: Enables organizations to share threat intelligence, including malware hashes, IP addresses, domains, and attack patterns.
    Correlation: Automatically correlates data to identify relationships between indicators of compromise (IOCs).
    Event Management: Tracks and organizes threat data into events for better context and analysis.
    Integration: Can integrate with other tools (e.g., TheHive) to enrich incident response efforts with actionable intelligence.
Cortex:
  Cortex is an analysis and automation engine that provides a set of analyzers for conducting automated tasks on observables (e.g., IPs, domains, files). Heres its features:
    Observable Analysis: Conducts in-depth analysis of observables (e.g., scans IPs for open ports, fetches WHOIS information, checks for reputation scores).
    Playbook Execution: Automates repetitive tasks to reduce analyst workload.
    Integration with TheHive: Analysts can send observables from TheHive to Cortex for automated analysis and receive results directly in TheHive.
    Scalability: Supports multiple analyzers and runs in a scalable environment to handle many tasks concurrently.

How to set it up:
  Please follow these documentations and video for installation and configuration. When configuring please use your devices ip address':
    Thehive:
      https://docs.strangebee.com/thehive/download/
    Cortex:
      https://docs.strangebee.com/cortex/installation-and-configuration/
    Misp:
      https://www.youtube.com/watch?v=HwSx_a3qQr0&t=380s
      https://www.youtube.com/watch?v=4870zcDL9Ek&t=602s
      

Network Setup:

Initially, to start the set up of this project, download the promox ISO image and burn it into a flashdrive.
Put the flashdrive into the physical hardware that you will be using for this SOC creation.
Boot the hardware up to the promox ISO image and install proxmox on the hardware.
After installation, displayed on the monitor should be a URL where you can connect to the proxmox server remotely. (Make sure the hardware has internet access)
After you have accessed the proxmox server, add the ISO images into the proxmox server. 
Once the ISO images have been added to proxmox, you can create new VMs.

First, before we create Any VMs, create 3 virtual bridges through proxmox.(vmbr0, vmbr1, vmbr2)
First start by creating a VM for OPNsense.
Once OPNsense is downloaded, configure it to handle two seperate lans.
For my project I used the subnets 192.168.1.0 and 192.168.2.0

Add the three bridges to the OPNsense router. Vmrb0 is used to connect to the WAN, vmbr1 is set to the 192.168.1.0 subnet and vmbr2 is set to the 192.168.2.0 subnet.
For my project I used the subnets 192.168.1.0 and 192.168.2.0

The subnet 192.168.1.0 is used to put our Wazuh stack and SOAR software.
The subnet 192.168.2.0 is used for our testing environment.

We can now create the rest of our VMs for this environment.
You can use the ubuntu ISO image to create two VMs with the bridge vmbr1. These will be used for the Wazuh software and SOAR software.

You can create 1 ubuntu and 1 Windows machine on the other subnet to use for testing purposes.
Make sure these two VMs have the bridge vmbr2.

To setup the Wazuh stack, follow Wazuh's documentation:
https://documentation.wazuh.com/current/installation-guide/wazuh-server/step-by-step.html

Follow this documentation on adding Wazuh to OPNsense and integrating it with the Wazuh manager:
https://help-cloudfence.eu.helpdocsite.com/opnsense-support/opnsense-wazuh-plugin

After setting up Wazuh and integrating it on OPNsense,
Surricata logs will now be sent to the Wazuh dashboard where you can visualize malicious traffic on the network.
