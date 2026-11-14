Task 4 – Install, Test and Fix

1\. Objective



The objective was to install the Orion-Layers policy package, test network connectivity and investigate how multiple Ordered Layers enforce Access Control decisions.



2\. Initial Installation



The policy installation was attempted on the gateway object A-GW-Cluster.



The installation could not be completed because the lab environment encountered a TCP connectivity failure.



A functional Security Gateway appliance was not available to receive and enforce the policy.



3\. Initial T1 Investigation



The assignment requires testing SSH connectivity from Admin\_PC to the Security Gateway.



This test was not performed because gateway installation and traffic forwarding were unavailable.



Expected Policy Behavior



The Network layer contains an Admin Access rule that permits SSH to the gateway.



However, the Service-Control layer initially permits HTTP, HTTPS, DNS and SMTP, but does not permit SSH.



If the connection reaches the Service-Control layer, its Cleanup Rule would drop the SSH traffic.



This demonstrates that an Accept action in the first Ordered Layer does not automatically permit traffic through the complete policy.



4\. Configuration Fix



An additional rule named Admin Services was added at position 1 of the Service-Control layer.



Setting	Value

Name	Admin Services

Source	Admin\_PC

Destination	A-GW-Cluster

Services	SSH, HTTPS

Action	Accept

Track	Log



The updated Service-Control rulebase became:



Position	Rule Name	Action

1	Admin Services	Accept

2	Allowed Services	Accept

3	Cleanup Rule	Drop



The configuration was published in SmartConsole.



5\. Traffic Test Results



The following tests were not performed because a functional Security Gateway appliance was unavailable.



Test	Traffic Description	Actual Result	Matching Layer/Rule

T1	Admin\_PC to Gateway using SSH	Not Performed	Not Available

T2	Internal host to external server using HTTP	Not Performed	Not Available

T3	Internal host to external server using Ping	Not Performed	Not Available

T4	Internal host to Gateway using Ping	Not Performed	Not Available

T5	Internal host to Web\_Server using Telnet	Not Performed	Not Available

6\. Technical Explanation



The policy is designed to evaluate traffic through the Ordered Layers in sequence.



The initial configuration permits SSH in the Network layer but does not permit SSH in the Service-Control layer.



The Admin Services rule addresses this configuration gap by explicitly permitting SSH and HTTPS from the administrator workstation to the gateway.



The actual runtime behavior could not be verified without a functioning Security Gateway.



7\. Conclusion



The Service-Control configuration was updated to include the Admin Services rule and published successfully.



Installation and traffic testing remain pending until a functional Security Gateway appliance becomes available.

