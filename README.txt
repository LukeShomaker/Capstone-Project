# Capstone-Project


This README encompasses Luke and Ajay's Senior capstone Cyber project!!


The overall goal of this project was to implement a working SOC and SOAR

What is a SOC?
SOC stands for Security Operation Center.

To create a SOC, one must implement multiple differnet pieces of software and integrate them  together in order to properly create the SOC


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

Wazuh Stack:
This stack manages the visualization software to see reports based on malicious traffic on the network.
A wazuh agent needs to be install on the OPNsense router to allow integration with the manager.
A wazuh agent is needed on endpoints that you want to collect data from.
The wazuh indexer deals with data manipulation.


SOAR Software:


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

