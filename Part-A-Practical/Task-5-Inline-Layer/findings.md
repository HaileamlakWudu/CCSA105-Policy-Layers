# Task 5 – Create the DMZ-Policy Inline Layer

## 1. Objective

The objective was to create a new Inline Layer named **DMZ-Policy** and attach it to the Internal to DMZ rule in the Network Ordered Layer.

The Inline Layer provides separate access control for the organization's DMZ web and mail servers.

## 2. General Settings

The following settings were configured:

| Setting | Configuration |
|---|---|
| Layer Name | DMZ-Policy |
| Comment | Controls access to DMZ resources |
| Firewall | Enabled |
| Applications & URL Filtering | Enabled |
| Content Awareness | Enabled |
| Mobile Access | Disabled |
| Sharing | Enabled |

## 3. Advanced Settings

| Setting | Configuration |
|---|---|
| Implicit Cleanup Action | Drop |

## 4. Permissions

The following profiles were retained with editing permissions:

- Super User
- Read-Write All

## 5. DMZ-Policy Rulebase

The following rules were configured:

| No. | Rule Name | Source | Destination | Services | Action | Track |
|---|---|---|---|---|---|---|
| 1 | Web Access | Any | Web_Server | HTTP, HTTPS | Accept | Log |
| 2 | Mail Access | Any | Mail_Server | SMTP | Accept | Log |
| 3 | Cleanup Rule | Any | Any | Any | Drop | Log |

### Rule Explanation

- **Web Access:** Allows HTTP and HTTPS traffic to the Web_Server.

- **Mail Access:** Allows SMTP traffic to the Mail_Server.

- **Cleanup Rule:** Drops traffic that does not match the permitted DMZ access rules.

## 6. Attach the Inline Layer

The Network Ordered Layer was modified to attach the DMZ-Policy Inline Layer to rule 3.

### Original Rule

| Setting | Original Configuration |
|---|---|
| Rule Name | Internal to DMZ |
| Source | Internal_LAN |
| Destination | DMZ_Net |
| Action | Accept |

### Updated Configuration

| Setting | Updated Configuration |
|---|---|
| Rule Name | Internal to DMZ |
| Source | Internal_LAN |
| Destination | DMZ_Net |
| Action | Inline Layer |
| Attached Layer | DMZ-Policy |
| Track | Log |

This configuration allows the DMZ-Policy rules to inspect traffic matching the parent Internal to DMZ rule.

## 7. Publishing and Verification

The DMZ-Policy Inline Layer was created, its rules were configured, and it was attached to the Network rulebase.

The configuration was published successfully in SmartConsole.

Runtime traffic enforcement was not verified because the Security Gateway appliance was unavailable.

## 8. Evidence

The following screenshots document the configuration:

- `T5-01-General-Settings.png`
- `T5-02-Advanced-Settings.png`
- `T5-03-Permissions-Settings.png`
- `T5-04-DMZ-Policy-Rulebase.png`
- `T5-05-Network-Inline-Rule.png`

## 9. Conclusion

The **DMZ-Policy Inline Layer** was successfully configured and attached to the Internal to DMZ rule.

This provides a separate rulebase for managing access to DMZ resources and demonstrates how Inline Layers organize more specific security requirements within a larger policy.
