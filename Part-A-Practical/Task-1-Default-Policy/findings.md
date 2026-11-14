# Task 1 – Explore the Default Policy and Layer

## 1. Objective

The objective was to explore the default Access Control policies in SmartConsole, identify their Ordered Layers, and examine the General, Advanced, and Permissions settings.

The explicit Cleanup rule action was also inspected.

## 2. Default Policy Packages

Two default Access Control policy packages were identified.

| Access Control Policy | Default Ordered Layer |
|---|---|
| Alpha-Standard | Alpha-Standard Network |
| Standard | Standard-Network |

## 3. General Settings

Both default Ordered Layers had the following configuration:

| Setting | Alpha-Standard Network | Standard-Network |
|---|---|---|
| Enabled Blades | Firewall | Firewall |
| Sharing | Disabled | Disabled |
| Applies To | Alpha-Standard | Standard |

## 4. Advanced Settings

| Setting | Alpha-Standard Network | Standard-Network |
|---|---|---|
| Implicit Cleanup Action | Drop | Drop |
| Proxy Configuration | Disabled | Disabled |
| Dynamic Layer | Disabled | Disabled |

## 5. Permissions

The following administrator profiles were identified as having editing permissions:

- Super User
- Read-Write All

These permissions were observed for the default layers.

## 6. Explicit Cleanup Rule

The explicit Cleanup rule in the inspected default policy rulebase had the following action:

| Setting | Observed Value |
|---|---|
| Cleanup Rule Action | Accept |

The explicit Cleanup rule action was **Accept**, while the Implicit Cleanup Action was **Drop**.

These are separate policy configuration settings.

## 7. Evidence

The following screenshots provide evidence of the inspected configurations:

- `T1-01-General-Settings.png`
- `T1-02-Advanced-Settings.png`
- `T1-03-Permissions-Settings.png`
- `T1-04-Cleanup-Rule.png`

## 8. Conclusion

The SmartConsole environment contained two default Access Control policy packages, each with its own Ordered Layer.

Both layers had Firewall enabled, Sharing disabled, and Drop configured as the Implicit Cleanup Action. The explicit Cleanup rule was observed with an Accept action.

This task provided an understanding of the default policy structure and layer configuration before creating the **Orion-Layers** package.
