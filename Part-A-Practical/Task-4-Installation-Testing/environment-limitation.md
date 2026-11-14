# Lab Environment Limitation – Gateway Installation and Traffic Testing

## 1. Environment Description

The practical assignment was performed using Check Point SmartConsole connected to the Security Management Server.

The configuration activities, including policy package creation, Ordered Layer configuration, rule creation, and Inline Layer configuration, were performed in SmartConsole.

## 2. Technical Limitation

A functional Security Gateway appliance was not available in the lab environment.

When attempting policy installation, the installation process encountered a TCP connectivity failure because the required gateway connectivity was unavailable.

As a result, the policy could not be installed on a functioning gateway.

## 3. Impact on Practical Testing

The following activities could not be verified:

- Policy installation on the Security Gateway.
- SSH connectivity testing.
- HTTP and ICMP traffic testing.
- Telnet traffic testing.
- Verification of actual firewall traffic logs.
- Runtime verification of Inline Layer enforcement.

## 4. Alternative Approach

The policy configurations were completed and documented in SmartConsole wherever possible.

Gateway-dependent activities are marked as **Not Performed (N/P)** rather than reporting assumed results.

## 5. Future Completion

When a functional Security Gateway appliance becomes available, the remaining installation and traffic-testing activities can be completed using the existing **Orion-Layers** policy package.
