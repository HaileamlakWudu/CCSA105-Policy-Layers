
# Part B – Theory Questions

## CCSA105 – Policy Layers (Module 5)

**Student Name:** Haileamlak Wudu Alene

**Registration ID:** C11/26/CCSA/17002

**Assignment:** Practical Assignment – Policy Layers

**Total Marks:** 30

---

# Section B1: Multiple Choice Questions (5 Marks)

### Q1. Which statement best describes a policy layer?

**Answer: B. A set of rules that divides a policy into smaller, more manageable sections.**

A policy layer is a collection of security rules that forms part of a larger Access Control policy. It helps administrators organize and manage security rules more efficiently.

### Q2. What are the names of the default Access Control policy and its default Ordered Layer?

**Answer: C. Standard and Network.**

The default Access Control policy is Standard, and its default Ordered Layer is Network.

### Q3. A packet matches an Accept rule in the first Ordered Layer. What does the gateway do next?

**Answer: A. It continues checking the next Ordered Layer.**

An Accept action in one Ordered Layer does not automatically allow the traffic through the entire policy. The packet must also pass the remaining applicable Ordered Layers.

### Q4. Which type of layer is attached to a specific rule as a sub-policy?

**Answer: D. Inline Layer.**

An Inline Layer is attached to a specific rule in another layer. It provides additional inspection and access control for traffic matching the parent rule.

### Q5. What is the recommended practice at the end of each Ordered Layer?

**Answer: B. Add an explicit Cleanup rule with the same Action as the Implicit Cleanup Rule.**

An explicit Cleanup rule makes the final policy decision visible and easier to understand, review and troubleshoot.

---

# Section B2: Short Answer Questions (15 Marks)

### Q6. Define a policy layer and state why layers are useful in a large network. Name two benefits of using them.

**Answer:**

A policy layer is a collection of Access Control rules that forms part of a larger security policy. It divides a large rulebase into smaller sections based on different security requirements.

Two benefits of using policy layers are:

1. **Better policy management:** Administrators can organize security rules into separate layers, making policies easier to understand, review and maintain.

2. **Improved administration:** Different administrators or teams can manage specific layers using permissions, reducing unnecessary access to the entire policy.

### Q7. Compare Ordered Layers and Inline Layers. For each, say how it is evaluated and give one use case.

**Answer:**

An **Ordered Layer** is evaluated as part of the main Access Control policy. Multiple Ordered Layers are checked sequentially according to their configured order. If a packet is dropped, evaluation stops. If it is accepted, evaluation continues to the next Ordered Layer.

**Use case:** A Network layer followed by a Service-Control layer to manage network access and permitted services.

An **Inline Layer** is attached to a specific rule inside another layer. When traffic matches the parent rule, the Inline Layer is evaluated to apply more specific security checks.

**Use case:** Attaching a DMZ-Policy layer to an Internal-to-DMZ rule to control access to web and mail servers.

### Q8. Describe the order of enforcement for Ordered Layers. Include what happens when a rule action is Drop, when it is Accept, and when no rule matches.

**Answer:**

Ordered Layers are evaluated sequentially from top to bottom according to their configured order.

- **Drop:** The packet is denied, and policy evaluation stops.
- **Accept:** The packet is allowed to continue to the next applicable Ordered Layer. It is finally permitted only if it passes the remaining policy checks.
- **No matching rule:** The layer's implicit cleanup behavior determines the result. If the Implicit Cleanup Action is Drop, the packet is dropped.

Therefore, traffic must pass all applicable Ordered Layers before it is permitted through the policy.

### Q9. Name the three groups of settings you configure for a layer. Give one example of a setting from each group.

**Answer:**

The three groups of layer settings are:

1. **General:** Includes the layer name, enabled security blades and Sharing setting.
2. **Advanced:** Includes the Implicit Cleanup Action, Proxy Configuration and Dynamic Layer settings.
3. **Permissions:** Defines which administrator profiles are allowed to edit the layer, such as Super User and Read-Write All.

### Q10. Explain what Sharing does for a layer. State one guideline from the module about sharing or reusing layers.

**Answer:**

Sharing allows a layer to be reused across multiple supported policy packages instead of creating separate copies of the same rules.

One guideline is to enable Sharing when a layer needs to be reused in multiple policy packages. This helps maintain consistent security rules, reduces duplication and makes policy administration easier.

---

# Section B3: Scenario Questions (10 Marks)

### Q11. A policy has two Ordered Layers. A connection is accepted by a rule in the first layer. The second layer has no rule that matches the connection and no explicit Cleanup rule, and its Implicit Cleanup Action is Drop. What happens to the connection? Explain how you would confirm this, how you would fix it if the connection should be allowed, and why an explicit Cleanup rule is recommended.

**Answer:**

The connection is dropped because the second Ordered Layer does not contain a matching Accept rule. Even though the first layer accepted the connection, the second layer still evaluates it and applies its Implicit Cleanup Action of Drop.

To confirm this, I would check the firewall logs in SmartConsole under Logs & Monitor and identify the layer responsible for dropping the connection.

To fix the problem, I would add an appropriate Accept rule in the second layer with the correct source, destination and service.

An explicit Cleanup rule is recommended because it makes the final decision visible in the rulebase, improves readability and makes troubleshooting easier.

### Q12. A company policy has grown to hundreds of rules. Administrators find it slow to review and are afraid to change it. Propose a layer design using Ordered and Inline Layers. Explain how your design improves manageability, role-based administration and performance.

**Answer:**

I would divide the large policy into several Ordered Layers based on their security responsibilities.

For example:

1. **Network Layer:** Controls network access between internal, external and DMZ networks.
2. **Service-Control Layer:** Controls permitted network services such as HTTP, HTTPS, DNS and SMTP.
3. **Application Layer:** Contains additional application-specific access controls where required.

I would also create Inline Layers for specific areas, such as a DMZ-Policy layer attached to the rule controlling access to DMZ servers.

This design improves the environment in three ways:

#### 1. Manageability

Administrators can work with smaller, organized rulebases instead of reviewing hundreds of rules in one large policy. This makes changes easier to understand and maintain.

#### 2. Role-Based Administration

Permission Profiles can restrict administrators to editing only the layers they are responsible for. For example, a DMZ administrator can be given permission to manage the DMZ-Policy layer without needing full access to the entire policy.

#### 3. Performance and Efficiency

A well-organized policy makes rule review, troubleshooting and administration more efficient. Rules can be arranged and optimized to avoid unnecessary processing. However, adding more layers does not automatically improve gateway performance, so the design should avoid unnecessary layers and excessive rules.

Overall, using Ordered and Inline Layers makes security policies easier to maintain, review and manage while supporting better administrative control.

---

# Conclusion

This theory section demonstrates an understanding of Check Point Policy Layers, including Ordered Layers, Inline Layers, policy enforcement, Cleanup rules, layer settings, permissions and Sharing.

The concepts covered in these answers are also reflected in the practical implementation of the Orion-Layers policy package, which includes the Network, Service-Control and DMZ-Policy layers.

---

# References

1. CCSA105 Module 5 – Policy Layers course slides.
2. Lab 5A – Configure Ordered Layers.
3. Lab 5B – Configure Inline Layers.
4. Check Point Quantum Security Management Administration Guide.
