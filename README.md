# Cisco-EEM-Auto-Export

*This is the readme markdown file for my first GitHub project. Thanks so much for the enablement of Cisco HK team on DevNET solution enablment throughout Year 2020.*

## Background
In typical network infrastructure design, network devices configuration /setting including routers, switches, firewall wireless controllers are maintained individually. There is no centralized location to store, backup, consolidate the setting, status, snapshot of these networking devices. 

This makes network administrators or vendors whom provide maintenance support difficult to understand the latest setting or status of the network devices in case of a device failure. 

## Cisco IOS Embedded Event Manager (EEM)
Starting from Cisco IOS version 12.3(4)T, 12.0(26)S in long time ago, Cisco introduced a feature called [Embedded Event Manager](https://www.cisco.com/c/en/us/products/ios-nx-os-software/ios-embedded-event-manager-eem/index.html) (EEM). The first version was EEM 1.0 version. EEM is a powerful and flexible subsystem that provides real-time network event detection and onboard automation. It gives you the ability to adapt the behavior of your network devices to align with your business needs.

## What Cisco-EEM-Auto-Export does?

This script is sets of CLI command to be input to Cisco IOS or IOS-XE routers or switches. This script will run regularly as service. EEM engine will trigger this script to run automatically according to the configured interval in this EEM script.

Once this script run, it will collect corresponding CLI command automatically and store the output to a local file and then store the file to a FTP server folder automatically.

## What IOS version and Devices can support this EEM script?

This script mainly utilizes "regexp" command in EEM command reference. According to Cisco command reference [Cisco EEM Command Reference](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/eem/command/eem-cr-book/eem-cr-a1.html#wp1168104291). Minimal IOS version version to run "regexp" command is 12.4(22)T or 12.2(33)SRE. According to Cisco [EEM version histroy](https://www.ciscolive.com/c/dam/r/ciscolive/emea/docs/2015/pdf/LABNMS-2001-LG.pdf), that command was introduced in EEM vesrion 3.0.

![Image](https://github.com/leonmflai/Cisco-EEM-Auto-Export/blob/master/regexp-ios-version.jpg)

![Image](https://github.com/leonmflai/Cisco-EEM-Auto-Export/blob/master/EEM%20Version%20History.jpg)

However, to run this script smoothly, we recommend you should run with the latest EEM version. Currently, it is EEM 4.0.

Currently, a variety of network devices including Cisco ISR-G2/4K, Catalyst 3650,3850,9300,4500 switch, Nexus 3K/7K/9K data center siwtch with IOS or NXOS version can support EEM 4.0. For example, Cisco Catalyst 9300 Switch with version Release Gibraltar-16.12.4 can support EEM 4.0.

For details of version and device compatiblity for EEM 4.0, please visit [Cisco Feature Netvigator](https://cfnng.cisco.com/)

## Installation

To install the script. Login to router or switch at "enable" mode and then "configure terminal" mode

### Enter Configure Terminal mode
```configure terminal```

### Input the script
''' event manager applet PM_Health_Check-To-FTP
 description PreventiveMaint_Health_Check-To-FTP
 event timer cron name Daily cron-entry "05 02 * * *"
 action 0.01  info type routername
 action 1.01 cli command "enable"
 action 1.02 cli command "show clock"
 action 1.03 regexp "(2[0-3]|[01][0-9]):([0-6][0-9]):([0-6][0-9])" "$_cli_result" time hour minute second
 action 1.04 puts "$time"
 action 1.05 puts "$hour"
 action 1.06 puts "$minute"
 action 1.07 puts "$second"
 action 1.11 cli command "show clock"
 action 1.12 regexp "(Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec) ([1-9]|0[1-9]|[1-2][0-9]|3[0-1]) (20[1-9][0-9])" "$_cli_result" time2 month day year
 action 1.13 puts "$time2"
 action 1.14 puts "$month"
 action 1.15 puts "$day"
 action 1.16 puts "$year"
 action 2.01 cli command "configure terminal"
 action 2.02 cli command "file prompt quiet"
 action 2.03 cli command "do copy run flash:$_info_routername-$year$month$day-$hour$minute$second.txt"
 action 2.04 cli command "do show inventory | append flash:$_info_routername-$year$month$day-$hour$minute$second.txt"
 action 2.05 cli command "do show version | append flash:$_info_routername-$year$month$day-$hour$minute$second.txt"
 action 2.06 cli command "do show process mem sorted | append flash:$_info_routername-$year$month$day-$hour$minute$second.txt"
 action 2.07 cli command "do show interface status | append flash:$_info_routername-$year$month$day-$hour$minute$second.txt"
 action 2.08 cli command "do show interface | append flash:$_info_routername-$year$month$day-$hour$minute$second.txt"
 action 2.09 cli command "do show clock | append flash:$_info_routername-$year$month$day-$hour$minute$second.txt"
 action 2.10 cli command "do copy flash:$_info_routername-$year$month$day-$hour$minute$second.txt ftp://{FTP_User}:{FTP_Password}@{FTP_Server}/$_info_routername-$year$month$day-$hour$minute$second.txt"
 action 3.01 cli command "file prompt alert"
 action 3.02 puts "$_info_routername-$year$month$day-$hour$minute$second.txt"
 action 4.01 syslog priority informational msg "Configuration change detected. Write to TFTP succesfully executed"'''

## Elaboration of Scripts

## Typical Network Diagram

## Virtual Environment for Testing




With latest API, configuration management tools like Python RestAPI, YANG, NetCONF, RestCONF, JSON/XML, Ansible, Puppet, Terraform, there are plenty of channels to retrieve the output, status, settings of the network devices. Some network management platform or plugin like Solarwinds NCM, ManageEngine Network Configuration Manager can support more advanced configuration management like regular configuration, setting backup or even execute configuration change in predefined schedule. 

Except leveraging API programming tools, most of the commercial available tools requires subscription charges or a upfront costing. 

With API programming tools, it still requires a software agent resides on a server, container or even a docker because utlitilizing off-box programming interfaces of network devices. Instead of having programming code outside the network devices, Cisco allows customer run simplified programming codes on their ISR routers, ASR Routers, Catalyst Switches, Nexus Switche or even some latest Catalyst 9800 wireless controllers.

For more information, please refer to following document:
Understanding Cisco EEM by examples Part 1
[Refence Link] https://learningnetwork.cisco.com/s/article/understanding-cisco-eem-by-examples-part-1 

This project and repo aims at scheduled configuration and status backup to a FTP server regulary. The filename of the backup will combines devices hostname as well as timestamp. I hope this will make networking guy start to understand more about value of coding and automation.


