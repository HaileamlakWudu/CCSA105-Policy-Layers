# Task 1 – Explore the Default Policy and Layer

## 1. Objective

The objective was to explore the default Access Control policies in Check Point SmartConsole, identify their Ordered Layers, and examine the General, Advanced, and Permissions settings.

The explicit Cleanup rule action was also inspected.

This task was initially completed in the home laboratory and subsequently verified in the cloud laboratory environment. Both environments were documented to demonstrate the configurations and identify any differences in policy naming.

## 2. Default Policy Packages

Two default Access Control policy packages were identified in each laboratory environment.

| Laboratory Environment | Access Control Policy | Default Ordered Layer |
|---|---|---|
| Home Lab | Alpha-Standard | Alpha-Standard Network |
| Home Lab | Standard | Standard-Network |
| Cloud Lab | Test | Test Network |
| Cloud Lab | Standard | Standard |

The policy package names and their corresponding default Ordered Layers differed between the two environments. However, the inspected configurations were similar.

## 3. General Settings

The inspected default Ordered Layers in both environments had the following configuration:

| Setting | Home Lab | Cloud Lab |
|---|---|---|
| Enabled Blades | Firewall | Firewall |
| Sharing | Disabled | Disabled |
| Applies To | Corresponding default policy package | Corresponding default policy package |

The General settings were consistent across both environments. Firewall was enabled, Sharing was disabled, and each default layer was associated with its respective policy package.

## 4. Advanced Settings

The following Advanced settings were observed in both laboratory environments:

| Setting | Home Lab | Cloud Lab |
|---|---|---|
| Implicit Cleanup Action | Drop | Drop |
| Proxy Configuration | Disabled | Disabled |
| Dynamic Layer | Disabled | Disabled |

Both environments used Drop as the Implicit Cleanup Action, with Proxy Configuration and Dynamic Layer disabled.

## 5. Permissions

The following administrator profiles were identified as having editing permissions on the inspected default layers in both environments:

- ICDFA-CCSA-PRACTICAL(only on the lab)
- Super User
- Read-Write All

The Permissions configurations were consistent between the two laboratory environments.

## 6. Explicit Cleanup Rule

The explicit Cleanup rule was inspected in the default policy rulebase.

| Setting | Home Lab | Cloud Lab |
|---|---|---|
| Explicit Cleanup Rule Action | Accept | Accept |

The explicit Cleanup rule action was observed as **Accept**, while the Implicit Cleanup Action was configured as **Drop**.

These are separate policy configuration settings and were documented independently.

## 7. Evidence

Evidence was collected from both laboratory environments.

### Home Lab Evidence

- `T1-01-General-Settings.png`
- `T1-02-Advanced-Settings.png`
- `T1-03-Permissions-Settings.png`
- `T1-04-Cleanup-Rule.png`

### Cloud Lab Evidence

The corresponding screenshots from the cloud laboratory demonstrate the default policy packages, layer settings, permissions, and Cleanup rule configuration.

Both sets of evidence are included in the repository to demonstrate the work performed and the verification carried out in the cloud environment.

## 8. Conclusion

The default Access Control policies were explored in both the home and cloud laboratory environments.

Although the policy package names and default Ordered Layer names differed, the inspected configurations were similar. Both environments had Firewall enabled, Sharing disabled, and Drop configured as the Implicit Cleanup Action. The Super User and Read-Write All administrator profiles had editing permissions.

The explicit Cleanup rule was observed with an Accept action, which differed from the Implicit Cleanup Action configured on the layers.

Completing this task in both environments provided an understanding of the default policy structure, layer configuration, cleanup behavior, and administrator permissions before proceeding with the creation of the custom `Orion-Layers` policy package.
