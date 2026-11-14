Task 7 – Layer Order and Sharing

1\. Objective



The objective was to investigate how the order of Ordered Layers affects traffic inspection and understand how Sharing allows an Inline Layer to be reused across policy packages.



2\. Original Layer Order



The original Orion-Layers policy order was:



Network

Service-Control



Network was the first Ordered Layer, followed by Service-Control.



3\. Changed Layer Order



The Service-Control layer was temporarily moved above Network.



The temporary order was:



Service-Control

Network



The new order was published in SmartConsole.



4\. Expected Effect on Traffic Inspection



When Ordered Layers are rearranged, the order in which traffic is inspected changes.



The expected outcomes for T3 and T4 are:



Test	Original Order	Changed Order

T3 – External Ping	Service-Control Cleanup Rule drops traffic after Network permits it through Outbound	Service-Control Cleanup Rule drops traffic first

T4 – Gateway Ping	Network Stealth Rule drops traffic	Service-Control Cleanup Rule drops traffic first



The final outcome for both tests is Drop.



The user experiences the same denial, although the responsible rule for T4 changes after the layer order is modified.



These outcomes are based on the configured policy rules and were not verified using gateway traffic logs.



5\. Restoring the Original Order



After examining the layer arrangement, the original order was restored:



Network

Service-Control



The restored configuration was published successfully in SmartConsole.



6\. Sharing Configuration



The DMZ-Policy Inline Layer was configured with Sharing Enabled.



Sharing allows a layer to be reused in multiple supported policy packages rather than recreating the same rules separately.



For example, the DMZ-Policy layer could be reused in an additional policy package named Orion-Branch.



This helps maintain consistent DMZ access controls and reduces duplicated configuration.



7\. Evidence

T7-01-Service-Control-First.png

T7-02-Restored-Layer-Order.png

T7-03-DMZ-Sharing-Enabled.png

8\. Conclusion



The Ordered Layers were temporarily rearranged and then restored to their original configuration.



The exercise demonstrates that layer order affects which rules inspect traffic first and that a Drop decision prevents further policy evaluation.



The Sharing setting on DMZ-Policy provides the ability to reuse the layer in supported policy packages, improving policy consistency and administration.



Runtime testing was deferred because a functional Security Gateway appliance was unavailable.

