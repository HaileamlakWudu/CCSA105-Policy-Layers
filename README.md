# CCSA105 – Policy Layers Practical Assignment

![Course](https://img.shields.io/badge/Course-CCSA105-blue)
![Platform](https://img.shields.io/badge/Platform-Check%20Point%20SmartConsole-green)
![Status](https://img.shields.io/badge/Documentation-Updated-brightgreen)

## Student Information

| Field | Details |
|---|---|
| Student Name | Haileamlak Wudu Alene |
| Registration ID | C11/26/CCSA/17002 |
| Course | CCSA105 – Policy Layers |
| Assignment | Practical Assignment: Policy Layers |
| Total Marks | 100 |

---

## 1. Introduction

This repository contains the practical and theoretical work completed for the CCSA105 Policy Layers assignment.

The assignment focuses on using Check Point SmartConsole to divide a large Access Control policy into smaller, manageable policy layers.

The practical implementation covers the creation and configuration of Ordered Layers, Inline Layers, security rules, layer sharing, policy installation and traffic testing.

The work was initially performed in a home laboratory environment where a functional Security Gateway was unavailable. A cloud laboratory with a functional Security Gateway subsequently became available, allowing policy installation and some runtime connectivity tests to be attempted.

This repository documents the configuration work, installation results, observed traffic test results, laboratory limitations and expected policy behavior. Actual observations are distinguished from expected outcomes and tests that remain unverified.

## 2. Learning Objectives

The main objectives of this assignment are to:

- Understand the Check Point policy layer concept.
- Create and configure Ordered Layers.
- Create and configure Inline Layers.
- Understand the order of policy enforcement.
- Configure Access Control rules and Cleanup rules.
- Understand layer sharing and permissions.
- Analyze the impact of layer order on traffic inspection.
- Install policy packages on a Security Gateway.
- Perform network connectivity tests.
- Analyze firewall logs and identify matching layers and rules.

## 3. Laboratory Environment

The practical assignment was completed across two laboratory environments.

### 3.1 Home Laboratory

The initial configuration work was performed using Check Point SmartConsole connected to the Security Management Server.

The home laboratory did not have a functional Security Gateway available for policy installation and runtime traffic testing. An installation attempt encountered a TCP connectivity failure.

The configuration work completed in this environment was retained as evidence.

### 3.2 Cloud Laboratory

A cloud laboratory with a functional Security Gateway subsequently became available.

The `Orion-Layers` policy package was successfully installed in the cloud environment. This allowed gateway-dependent testing to begin.

However, some connectivity tests did not produce successful connections or corresponding firewall log entries. These results are documented individually rather than being presented as confirmed policy enforcement outcomes.

### 3.3 Main Components

| Component | Description |
|---|---|
| Management Platform | Check Point Security Management Server |
| Management Interface | SmartConsole |
| Policy Package | Orion-Layers |
| Gateway Object | Cloud Security Gateway object configured in SmartConsole |
| Network Layer | Network |
| Service Layer | Service-Control |
| Inline Layer | DMZ-Policy |

### Network Objects

| Object | Type | IP Address / Network |
|---|---|---|
| Internal_LAN | Network | 10.1.1.0/24 |
| DMZ_Net | Network | 172.16.10.0/24 |
| Admin_PC | Host | 10.1.1.101 |
| Web_Server | Host | 172.16.10.20 |
| Mail_Server | Host | 172.16.10.25 |

**Note:** The cloud test environment may use different source addresses from the private IP addresses defined in the policy objects. The actual source address observed by the Security Gateway is important when interpreting firewall rule matching.

## 4. Policy Architecture

The `Orion-Layers` policy package contains two Ordered Layers and one Inline Layer.

### Ordered Layer 1: Network

Responsible for network-level access control.

Rules include:

1. Admin Access
2. Stealth Rule
3. Internal to DMZ
4. Outbound
5. Cleanup Rule

### Ordered Layer 2: Service-Control

Responsible for controlling permitted network services.

Rules include:

1. Admin Services
2. Allowed Services
3. Cleanup Rule

The `Admin Services` rule permits SSH and HTTPS from the configured `Admin_PC` object to the Security Gateway.

The rule's source-address condition must match the actual source address observed by the gateway for the traffic to be accepted.

### Inline Layer: DMZ-Policy

Attached to the `Internal to DMZ` rule in the `Network` layer.

Rules include:

1. Web Access
2. Mail Access
3. Cleanup Rule

The Inline Layer provides additional inspection of traffic matching the parent `Internal to DMZ` rule.

## 5. Assignment Tasks

| Task | Description | Status |
|---|---|---|
| Task 1 | Explore Default Policy and Layer | Completed |
| Task 2 | Create Orion-Layers and Network Layer | Completed |
| Task 3 | Create Service-Control Ordered Layer | Completed |
| Task 4 | Install, Test and Fix | Installation successful in cloud; T1 attempted but SSH timed out due to source-address mismatch |
| Task 5 | Create DMZ-Policy Inline Layer | Completed |
| Task 6 | Install and Verify Inline Layer | Installation successful; T6 attempted but HTTP timed out; T7–T9 pending |
| Task 7 | Layer Order and Sharing | Configuration completed; runtime comparison not verified |
| Part B | Theory Questions | Prepared |

## 6. Installation and Traffic Testing Results

### 6.1 Policy Installation

The `Orion-Layers` policy package was successfully published and installed on the cloud Security Gateway.

The updated policy package, including the `DMZ-Policy` Inline Layer, was also successfully installed.

This confirms successful policy installation in the cloud environment. It does not independently confirm that individual traffic tests were accepted or dropped as expected.

### 6.2 Task 4 – Initial SSH Test

An SSH connection was attempted from the cloud laboratory to the Security Gateway.

The configured `Admin Services` rule expected traffic from `Admin_PC` with private IP address `10.1.1.101`.

However, the cloud connection was observed by the gateway with a public/NAT source address rather than the expected private address.

The SSH connection timed out, and the source-address mismatch prevented the traffic from matching the intended `Admin Services` rule.

The applicable firewall logs should be used to establish the exact blocking layer and rule for each connection attempt.

### 6.3 Task 6 – Inline Layer Traffic Test

An HTTP connection was attempted from the cloud Windows workstation to `Web_Server` (`172.16.10.20`) using TCP port 80.

Command executed:

```powershell
curl.exe -v --connect-timeout 5 http://172.16.10.20/
```

The connection timed out after approximately five seconds.

No corresponding firewall log entry was found in SmartConsole Logs & Monitor. Consequently, the exact reason for the timeout and the matching policy layer or rule could not be established.

The remaining tests are:

| Test | Traffic | Current Status |
|---|---|---|
| T7 | Internal host → Mail_Server, SMTP (TCP 25) | Not yet tested |
| T8 | Internal host → Web_Server, Telnet (TCP 23) | Not yet tested |
| T9 | Internal host → External server, HTTP | Not yet tested |

### 6.4 Task 7 – Layer Order Testing

The `Service-Control` layer was temporarily moved above the `Network` layer and the original order was subsequently restored.

The expected policy behavior was analyzed for T3 (External Ping) and T4 (Gateway Ping).

The expected final action for both tests is Drop, but the responsible layer and rule can differ depending on the order of the Ordered Layers.

The actual T3 and T4 outcomes under the temporary arrangement have not been verified through gateway logs.

## 7. Laboratory Limitations and Verification Status

### 7.1 Home Laboratory Limitation

During the initial home-lab work, a functional Security Gateway appliance was unavailable.

An attempt to install the policy encountered a TCP connectivity failure. Therefore, runtime traffic testing and gateway log verification could not be completed in that environment.

The SmartConsole configuration work was retained as evidence.

### 7.2 Cloud Laboratory Progress

The cloud laboratory resolved the original gateway-availability limitation.

The policy package was successfully installed, and runtime connectivity tests were attempted.

However, the tests revealed additional environment-related limitations:

- The SSH source address observed by the cloud gateway did not match the configured private `Admin_PC` address.
- The HTTP connection to `Web_Server` timed out.
- No corresponding firewall log was found for the T6 HTTP attempt.
- The remaining T7–T9 tests have not yet been performed.
- The temporary Task 7 layer-order comparison has not been confirmed through traffic logs.

### 7.3 Reporting Method

This repository distinguishes three types of information:

1. **Actual results:** Results directly observed during configuration, installation or testing.
2. **Expected behavior:** Outcomes predicted from the configured policy rules but not confirmed by actual traffic testing.
3. **Unverified results:** Tests that were not performed or for which sufficient logs were unavailable.

No simulated traffic logs, fabricated test results or assumed successful connections are presented as actual observations.

## 8. Repository Structure

```text
CCSA105-Policy-Layers/
│
├── README.md
├── .gitignore
│
├── Part-A-Practical/
│   │
│   ├── Task-1-Default-Policy/
│   │
│   ├── Task-2-Network-Layer/
│   │
│   ├── Task-3-Service-Control/
│   │
│   ├── Task-4-Installation-Testing/
│   │   ├── findings.md
│   │   ├── lab-limitation.md
│   │   └── evidence/
│   │
│   ├── Task-5-Inline-Layer/
│   │
│   ├── Task-6-Inline-Verification/
│   │   ├── findings.md
│   │ 
│   │
│   └── Task-7-Layer-Order-Sharing/
│       ├── findings.md
│       └── evidence/
│
└── Part-B-Theory/
    └── answers.md
```

Each practical task contains written documentation and an evidence directory for labelled SmartConsole screenshots, terminal outputs and other relevant laboratory evidence.

## 9. Technologies and Concepts

- Check Point SmartConsole
- Check Point Security Management
- Security Gateway
- Access Control Policy
- Policy Packages
- Ordered Layers
- Inline Layers
- Firewall Rules
- Explicit Cleanup Rules
- Implicit Cleanup Actions
- Policy Sharing
- Permission Profiles
- Policy Installation
- Firewall Logging
- Network Connectivity Testing

## 10. Conclusion

This assignment demonstrates the configuration and management of Check Point Access Control policy layers.

The practical work covers policy package creation, Ordered Layer configuration, Inline Layer integration, rulebase organization, policy installation, layer sharing and analysis of traffic inspection order.

The initial home-lab environment did not provide a functional Security Gateway, but the subsequent cloud laboratory allowed successful installation of the `Orion-Layers` policy package and the updated `DMZ-Policy` Inline Layer.

Runtime testing was also initiated. The SSH test exposed a source-address mismatch between the configured administrator object and the source address observed by the cloud gateway. The HTTP test to the Web Server timed out without a corresponding firewall log.

The remaining traffic tests and some layer-order comparisons require additional verification.

Overall, the assignment documents both the completed configuration work and the actual limitations encountered during runtime testing, while distinguishing verified results from expected policy behavior.

## 11. References

1. CCSA105 Module 5 course slides.
2. Check Point Quantum Security Management Administration Guide.
