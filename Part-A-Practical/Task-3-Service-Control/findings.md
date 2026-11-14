# Task 3 – Create the Service-Control Ordered Layer

## 1. Objective

The objective of this task was to create a second Ordered Layer named **Service-Control** within the Orion-Layers policy package.

This layer provides service-level access control by allowing selected network services and dropping traffic that does not match the permitted rules.

## 2. General Settings

The Service-Control layer was configured with the following settings:

| Setting | Configuration |
|---|---|
| Layer Name | Service-Control |
| Comment | Controls permitted network services |
| Firewall | Enabled |
| Applications & URL Filtering | Disabled |
| Content Awareness | Disabled |
| Mobile Access | Disabled |
| Sharing | Disabled |

Only the Firewall blade was enabled.

## 3. Advanced Settings

| Setting | Configuration |
|---|---|
| Implicit Cleanup Action | Drop |
| Proxy Configuration | Disabled |
| Dynamic Layer | Disabled |

## 4. Permissions

The following administrator profiles were retained with editing permissions:

- Super User
- Read-Write All

## 5. Ordered Layer Position

The Service-Control layer was added as the second Ordered Layer in the Orion-Layers policy package.

The original order was:

1. Network
2. Service-Control

## 6. Service-Control Rulebase

The following rules were created:

| No. | Rule Name | Source | Destination | Services | Action | Track |
|---|---|---|---|---|---|---|
| 1 | Allowed Services | Any | Any | HTTP, HTTPS, DNS (UDP and TCP), SMTP | Accept | Log |
| 2 | Cleanup Rule | Any | Any | Any | Drop | Log |

### Rule Explanation

- **Allowed Services:** Permits the specified network services, including web traffic, DNS queries, and SMTP.

- **Cleanup Rule:** Drops traffic that does not match the permitted service rule.

## 7. Publishing and Verification

The Service-Control layer was configured, added below Network, and published successfully in SmartConsole.

Gateway installation and runtime traffic testing were deferred because the functional Security Gateway appliance was unavailable.

## 8. Evidence

The following screenshots document the configuration:

- `T3-01-General-Settings.png`
- `T3-02-Advanced-Settings.png`
- `T3-03-Permissions-Settings.png`
- `T3-04-Layer-Order.png`
- `T3-05-Service-Control-Rulebase.png`

## 9. Conclusion

The **Service-Control Ordered Layer** was successfully created and configured.

It provides a separate rulebase for controlling permitted network services and improves the organization of the overall Access Control policy.
