CCSA105 – Policy Layers Practical Assignment



!Course !Module !Platform !Status



Student Information

Field	Details

Student Name	Haileamlak Wudu Alene

Registration ID	C11/26/CCSA/17002

Course	CCSA105 – Policy Layers

Module	Module 5

Assignment	Practical Assignment: Policy Layers

Total Marks	100

1\. Introduction



This repository contains the practical and theoretical work completed for the CCSA105 Policy Layers assignment.



The assignment focuses on using Check Point SmartConsole to divide a large Access Control policy into smaller, manageable policy layers.



The practical implementation covers the creation and configuration of Ordered Layers, Inline Layers, security rules, layer sharing and policy management.



The repository also documents the laboratory environment limitation that prevented full Security Gateway installation and runtime traffic testing.



2\. Learning Objectives



The main objectives of this assignment are to:



Understand the Check Point policy layer concept.

Create and configure Ordered Layers.

Create and configure Inline Layers.

Understand the order of policy enforcement.

Configure Access Control rules and Cleanup rules.

Understand layer sharing and permissions.

Analyze the impact of layer order on traffic inspection.

Understand policy installation and traffic log verification.

3\. Laboratory Environment

Component	Description

Management Platform	Check Point Security Management Server

Management Interface	SmartConsole

Policy Package	Orion-Layers

Gateway Object	A-GW-Cluster

Network Layer	Network

Service Layer	Service-Control

Inline Layer	DMZ-Policy

Network Objects

Object	Type	IP Address / Network

Internal\_LAN	Network	10.1.1.0/24

DMZ\_Net	Network	172.16.10.0/24

Admin\_PC	Host	10.1.1.101

Web\_Server	Host	172.16.10.20

Mail\_Server	Host	172.16.10.25

4\. Policy Architecture



The Orion-Layers policy package contains two Ordered Layers and one Inline Layer.



Ordered Layer 1: Network



Responsible for network-level access control.



Rules include:



Admin Access

Stealth Rule

Internal to DMZ

Outbound

Cleanup Rule

Ordered Layer 2: Service-Control



Responsible for controlling permitted network services.



Rules include:



Admin Services

Allowed Services

Cleanup Rule

Inline Layer: DMZ-Policy



Attached to the Internal to DMZ rule in the Network layer.



Rules include:



Web Access

Mail Access

Cleanup Rule

5\. Assignment Tasks

Task	Description	Status

Task 1	Explore Default Policy and Layer	Completed

Task 2	Create Orion-Layers and Network Layer	Completed

Task 3	Create Service-Control Ordered Layer	Completed

Task 4	Install, Test and Fix	Deferred

Task 5	Create DMZ-Policy Inline Layer	Completed

Task 6	Install and Verify Inline Layer	Deferred

Task 7	Layer Order and Sharing	Configuration completed; gateway tests deferred

Part B	Theory Questions	Prepared

6\. Laboratory Limitation



A functional Security Gateway appliance was not available during the laboratory exercise.



An attempt to install the policy encountered a TCP connectivity failure.



Consequently, gateway-dependent activities could not be completed, including:



Successful policy installation.

SSH, HTTP, ICMP and Telnet traffic testing.

Runtime verification of Inline Layer enforcement.

Collection of actual firewall traffic logs.



The policy configurations were completed in SmartConsole wherever possible.



Activities requiring a functional gateway are identified as deferred or not performed. No simulated traffic logs or assumed installation results are presented as actual results.



7\. Repository Structure

text

Part-A-Practical/

&#x20;   Task-1-Default-Policy/

&#x20;   Task-2-Network-Layer/

&#x20;   Task-3-Service-Control/

&#x20;   Task-4-Installation-Testing/

&#x20;   Task-5-Inline-Layer/

&#x20;   Task-6-Inline-Verification/

&#x20;   Task-7-Layer-Order-Sharing/



Part-B-Theory/

&#x20;   answers.md





Each practical task includes written documentation and an evidence directory for labelled SmartConsole screenshots.



8\. Technologies and Concepts

Check Point SmartConsole

Check Point Security Management

Access Control Policy

Ordered Layers

Inline Layers

Firewall Rules

Implicit Cleanup Action

Explicit Cleanup Rules

Policy Sharing

Permission Profiles

Firewall Logging

9\. Conclusion



This assignment demonstrates the configuration and management of Check Point Access Control policy layers.



The practical work covers policy package creation, Ordered Layer configuration, Inline Layer integration, rulebase organization and layer sharing.



Although runtime verification was limited by the absence of a functional Security Gateway appliance, the available configuration activities and theoretical concepts were documented.



10\. References

CCSA105 Module 5 course slides.

Lab 5A: Configure Ordered Layers.

Lab 5B: Configure Inline Layers.

Check Point Quantum Security Management Administration Guide.

