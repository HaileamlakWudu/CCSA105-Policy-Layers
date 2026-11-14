# Task 7 – Layer Order and Sharing

## 1. Objective

The objective of this task was to investigate how the order of Ordered Layers affects network traffic inspection and understand how the Sharing setting allows an Inline Layer to be reused across supported policy packages.

The task involved temporarily changing the order of the `Network` and `Service-Control` layers, examining the expected effect on traffic evaluation, restoring the original order, and reviewing the Sharing configuration of the `DMZ-Policy` Inline Layer.

## 2. Original Layer Order

The original `Orion-Layers` policy package contained two Ordered Layers in the following order:

1. `Network`
2. `Service-Control`

The `Network` layer was positioned first, followed by the `Service-Control` layer.

Under this arrangement, traffic was evaluated by the `Network` layer before continuing to the `Service-Control` layer, provided that no earlier rule terminated the evaluation with a Drop decision.

## 3. Changed Layer Order

For this task, the `Service-Control` layer was temporarily moved above the `Network` layer.

The temporary order was:

1. `Service-Control`
2. `Network`

The modified arrangement was published in SmartConsole.

This change altered the sequence in which traffic was inspected. The first Ordered Layer could now accept or drop traffic before the second layer evaluated it.

## 4. Expected Effect on Traffic Inspection

Changing the order of Ordered Layers changes which rules are evaluated first. A matching Drop rule terminates policy evaluation, while an Accept decision allows evaluation to continue through the remaining applicable Ordered Layers.

Based on the configured rules, the expected outcomes for T3 and T4 are:

| Test | Original Order: Network → Service-Control | Changed Order: Service-Control → Network | Expected Final Action |
|---|---|---|---|
| T3 – External Ping | Network Outbound rule permits traffic to continue; Service-Control Cleanup Rule drops it | Service-Control Cleanup Rule drops traffic before Network is evaluated | Drop |
| T4 – Gateway Ping | Network Stealth Rule drops traffic before Service-Control is evaluated | Service-Control Cleanup Rule drops traffic before Network is evaluated | Drop |

### T3 – External Ping

With the original order, the `Network` layer's Outbound rule is expected to allow the traffic to continue. The traffic then reaches the `Service-Control` layer, where ICMP is not included in the permitted services and is expected to be dropped by the Cleanup Rule.

After moving `Service-Control` above `Network`, the same traffic is expected to be dropped by the `Service-Control` Cleanup Rule before reaching the `Network` layer.

### T4 – Gateway Ping

With the original order, the `Network` layer's Stealth Rule is expected to drop traffic destined for the Security Gateway.

After moving `Service-Control` above `Network`, the traffic is expected to be dropped by the `Service-Control` Cleanup Rule first, provided that the source, destination and service do not match another accepting rule.

### Interpretation

The expected final action for both tests remains **Drop** under both layer arrangements.

However, the responsible layer and rule can change depending on the order.

This demonstrates that changing the order of Ordered Layers can change the enforcement point even when the final user-visible result remains the same.

**Verification status:** These outcomes are based on the configured policy rules. Actual traffic results for the temporary layer arrangement have not been established from gateway logs in the available evidence.

## 5. Restoring the Original Order

After examining the temporary arrangement, the original layer order was restored:

1. `Network`
2. `Service-Control`

The restored configuration was published successfully in SmartConsole.

The original arrangement was retained as the intended final policy configuration.

## 6. Sharing Configuration

The `DMZ-Policy` Inline Layer was configured with Sharing enabled.

Sharing allows an Inline Layer to be reused in multiple supported policy packages instead of requiring administrators to recreate equivalent rules separately.

For example, the existing `DMZ-Policy` layer could be reused in another policy package named `Orion-Branch`, subject to the platform's sharing and compatibility requirements.

This provides several administrative benefits:

- Reduces duplicated policy configuration.
- Helps maintain consistent DMZ access controls across policy packages.
- Makes centralized rule maintenance easier.
- Reduces the risk of inconsistent rule changes between packages.

Enabling Sharing does not itself prove that the Inline Layer has been reused in another package. It establishes the configuration needed to support reuse.

## 7. Evidence

The following screenshots document the Task 7 configuration:

| Evidence File | Description |
|---|---|
| `T7-01-Service-Control-First.png` | SmartConsole showing the temporary order with Service-Control above Network |
| `T7-02-Restored-Layer-Order.png` | SmartConsole showing the restored original order: Network followed by Service-Control |
| `T7-03-DMZ-Sharing-Enabled.png` | DMZ-Policy Inline Layer settings showing Sharing enabled |

If traffic tests were performed during the temporary arrangement, the corresponding T3 and T4 firewall logs should also be included to establish the actual matching layers and rules.

## 8. Conclusion

The Ordered Layers in the `Orion-Layers` policy package were temporarily rearranged, and the original order was subsequently restored.

The exercise demonstrates that Ordered Layer position affects the sequence of policy inspection and can change which rule enforces a traffic decision.

Based on the configured policy, T3 and T4 are expected to be dropped under both arrangements, although the responsible layer and rule may differ.

The `DMZ-Policy` Inline Layer was configured with Sharing enabled, allowing it to be reused in supported policy packages and helping maintain consistent security controls.

The cloud lab provided a functional Security Gateway, and the updated policy package was successfully installed during Task 6. However, the available evidence does not establish that T3 and T4 were actually retested under the temporary Task 7 layer arrangement. Therefore, the layer-order traffic comparison remains an expected policy analysis rather than a verified runtime result.
