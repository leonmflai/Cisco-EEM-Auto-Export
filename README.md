# Cisco-EEM-Auto-Export

*This is the readme markdown file for my first GitHub project. Thanks so much for the enablement of Cisco HK team on DevNET solution enablment throughout Year 2020.*

## Background
In typical network infrastructure design, network devices configuration /setting including routers, switches, firewall wireless controllers are maintained individually. There is no centralized location to store, backup, consolidate the setting, status, snapshot of these networking devices. 

This makes network administrators or vendors whom provide maintenance support difficult to understand the latest setting or status of the network devices in case of a device failure. 

## Cisco IOS Embedded Event Manager (EEM)
Starting from Cisco IOS version 12.3(4)T, 12.0(26)S in long time ago, Cisco introduced a feature called [Embedded Event Manager] (https://www.cisco.com/c/en/us/products/ios-nx-os-software/ios-embedded-event-manager-eem/index.html) (EEM). EEM is a powerful and flexible subsystem that provides real-time network event detection and onboard automation. It gives you the ability to adapt the behavior of your network devices to align with your business needs.

## What Cisco-EEM-Auto-Export does?



## What IOS version and Devices can support this EEM script?



## Installation

## Elaboration of Scripts


## Virtual Environment for Testing




With latest API, configuration management tools like Python RestAPI, YANG, NetCONF, RestCONF, JSON/XML, Ansible, Puppet, Terraform, there are plenty of channels to retrieve the output, status, settings of the network devices. Some network management platform or plugin like Solarwinds NCM, ManageEngine Network Configuration Manager can support more advanced configuration management like regular configuration, setting backup or even execute configuration change in predefined schedule. 

Except leveraging API programming tools, most of the commercial available tools requires subscription charges or a upfront costing. 

With API programming tools, it still requires a software agent resides on a server, container or even a docker because utlitilizing off-box programming interfaces of network devices. Instead of having programming code outside the network devices, Cisco allows customer run simplified programming codes on their ISR routers, ASR Routers, Catalyst Switches, Nexus Switche or even some latest Catalyst 9800 wireless controllers.

For more information, please refer to following document:
Understanding Cisco EEM by examples Part 1
[Refence Link] https://learningnetwork.cisco.com/s/article/understanding-cisco-eem-by-examples-part-1 

This project and repo aims at scheduled configuration and status backup to a FTP server regulary. The filename of the backup will combines devices hostname as well as timestamp. I hope this will make networking guy start to understand more about value of coding and automation.


