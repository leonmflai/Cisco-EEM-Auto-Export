# Cisco-EEM-Auto-Export

This is the readme file for my first GitHub project

*Cisco-EEM-Auto-Export
*In typical network infrastructure design, network devices configuration /setting including routers, switches , , wireless controllers are maintained individually. There is no *centralized location to store, backup, consolidate the setting, status, snapshot of these networking devices. 

With latest API, configuration management tools like Python RestAPI, YANG, NetCONF, RestCONF, JSON/XML, Ansible, Puppet, Terraform, there are plenty of channels to retrieve the output, status, settings of the network devices. Some network management platform or plugin like Solarwinds NCM, ManageEngine Network Configuration Manager can support more advanced configuration management like regular configuration, setting backup or even execute configuration change in predefined schedule. 

Except leveraging API programming tools, most of the commercial available tools requires subscription charges or a upfront costing. 

With API programming tools, it still requires a software agent resides on a server, container or even a docker because utlitilizing off-box programming interfaces of network devices. Instead of having programming code outside the network devices, Cisco allows customer run simplified programming codes on their ISR routers, ASR Routers, Catalyst Switches, Nexus Switche or even some latest Catalyst 9800 wireless controllers.

For more information, please refer to following document:
Understanding Cisco EEM by examples Part 1
[Refence Link] https://learningnetwork.cisco.com/s/article/understanding-cisco-eem-by-examples-part-1 

This project and repo aims at scheduled configuration and status backup to a FTP server regulary. The filename of the backup will combines devices hostname as well as timestamp. I hope this will make networking guy start to understand more about value of coding and automation.


