# Task 2 – Create Orion-Layers and Build the Network Layer

## 1. Objective

The objective of this task was to create a new Check Point Access Control policy package named **Orion-Layers** and configure its first Ordered Layer, named **Network**.

The Network layer was designed to control administrator access, protect the Security Gateway, manage internal network traffic, and provide an explicit Cleanup rule.

The configuration was initially completed in the home laboratory and subsequently implemented in the cloud laboratory. Both environments were configured and documented, with the cloud environment also providing the opportunity to perform successful policy installation.

## 2. Policy Package Configuration

A new policy package named **Orion-Layers** was created in SmartConsole with the following configuration:

| Setting | Configuration |
|---|---|
| Policy Package | Orion-Layers |
| Policy Type | Access Control |
| Ordered Layer | Network |
| Firewall Blade | Enabled |
| Sharing | Disabled |

The existing network objects were checked and reused where available. No unnecessary duplicate objects were created.

### Network Objects

| Object Name | Object Type | IP Address / Network |
|---|---|---|
| Internal_LAN | Network | 10.1.1.0/24 |
| DMZ_Net | Network | 172.16.10.0/24 |
| Admin_PC | Host | 10.1.1.101 |
| Web_Server | Host | 172.16.10.20 |
| Mail_Server | Host | 172.16.10.25 |
| A-GW-Cluster | Gateway | Existing gateway object |

## 3. Network Layer Rulebase

The Network Ordered Layer was configured with five rules.

| No. | Rule Name | Source | Destination | Services | Action | Track |
|---|---|---|---|---|---|---|
| 1 | Admin Access | Admin_PC | A-GW-Cluster | SSH, HTTPS | Accept | Log |
| 2 | Stealth Rule | Any | A-GW-Cluster | Any | Drop | Log |
| 3 | Internal to DMZ | Internal_LAN | DMZ_Net | Any | Accept | Log |
| 4 | Outbound | Internal_LAN | Any | Any | Accept | Log |
| 5 | Cleanup Rule | Any | Any | Any | Drop | Log |

## 4. Rule Explanation

- **Admin Access:** Allows the administrator workstation to access the Security Gateway through SSH and HTTPS.

- **Stealth Rule:** Drops other traffic directed to the gateway.

- **Internal to DMZ:** Initially permits traffic from the internal network to the DMZ. This rule is later changed to use the DMZ-Policy Inline Layer in Task 5.

- **Outbound:** Allows traffic originating from the internal network to other destinations.

- **Cleanup Rule:** Explicitly drops traffic that reaches the final rule without matching an earlier rule.

All five rules were configured with Log tracking.

## 5. Publishing and Policy Installation

The Network layer rulebase was completed and published successfully in both laboratory environments.

In the home laboratory, the configuration was completed and documented.

In the cloud laboratory, a functional Security Gateway was available. The Orion-Layers policy package was successfully installed on the gateway.

This confirmed that the policy configuration could be installed successfully in an operational gateway environment.

## 6. Evidence

Evidence was collected from both laboratory environments.

### Home Lab Evidence

- `T2-01-Orion-Layers-Package.png`
- `T2-02-Network-Rulebase.png`

### Cloud Lab Evidence

The corresponding cloud laboratory screenshots demonstrate:

- The Orion-Layers policy package.
- The configured Network Ordered Layer and its five rules.
- Successful policy installation on the Security Gateway.

Both sets of evidence are included in the repository to demonstrate the configuration work and its successful deployment in the cloud environment.

## 7. Conclusion

The **Orion-Layers** Access Control policy package and its first Ordered Layer, **Network**, were successfully configured in both laboratory environments.

The five rules organize network-level access control, administrator access, gateway protection, internal-to-DMZ communication, outbound traffic, and explicit cleanup behavior.

Unlike the initial home laboratory implementation, the cloud laboratory provided a functional Security Gateway, allowing the policy package to be successfully installed.

Task 2 was therefore completed, including configuration, publishing, and successful cloud gateway policy installation.
