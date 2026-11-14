Task 2 – Create Orion-Layers and Build the Network Layer

1\. Objective



The objective of this task was to create a new Check Point Access Control policy package named Orion-Layers and configure its first Ordered Layer, named Network.



The Network layer was designed to control administrator access, protect the Security Gateway, manage internal network traffic and provide an explicit Cleanup rule.



2\. Policy Package Configuration



A new policy package was created in SmartConsole with the following details:



Setting	Configuration

Policy Package	Orion-Layers

Policy Type	Access Control

Ordered Layer	Network

Firewall Blade	Enabled

Sharing	Disabled



The existing network objects were checked and reused. No duplicate network objects were created.



Network Objects

Object Name	Object Type	IP Address / Network

Internal\_LAN	Network	10.1.1.0/24

DMZ\_Net	Network	172.16.10.0/24

Admin\_PC	Host	10.1.1.101

Web\_Server	Host	172.16.10.20

Mail\_Server	Host	172.16.10.25

A-GW-Cluster	Gateway	Existing gateway object

3\. Network Layer Rulebase



The Network Ordered Layer was configured with five rules.



No.	Rule Name	Source	Destination	Services	Action	Track

1	Admin Access	Admin\_PC	A-GW-Cluster	SSH, HTTPS	Accept	Log

2	Stealth Rule	Any	A-GW-Cluster	Any	Drop	Log

3	Internal to DMZ	Internal\_LAN	DMZ\_Net	Any	Accept	Log

4	Outbound	Internal\_LAN	Any	Any	Accept	Log

5	Cleanup Rule	Any	Any	Any	Drop	Log

4\. Rule Explanation

Admin Access: Allows the administrator workstation to access the Security Gateway through SSH and HTTPS.

Stealth Rule: Drops other traffic directed to the gateway.

Internal to DMZ: Initially permits traffic from the internal network to the DMZ. This rule is later changed to use the DMZ-Policy Inline Layer in Task 5.

Outbound: Allows traffic originating from the internal network to other destinations.

Cleanup Rule: Explicitly drops traffic that reaches the final rule without matching an earlier rule.



All five rules were configured with Log tracking.



5\. Publishing and Verification



The Network layer rulebase was completed and published successfully in SmartConsole.



Policy installation and runtime traffic verification were deferred because a functional Security Gateway appliance was unavailable.



6\. Evidence



The following screenshots document the configuration:



T2-01-Orion-Layers-Package.png

T2-02-Network-Rulebase.png

7\. Conclusion



The Orion-Layers policy package and Network Ordered Layer were successfully configured. The five rules organize network-level access control and provide explicit logging and cleanup behavior. The configuration was published successfully in SmartConsole.

