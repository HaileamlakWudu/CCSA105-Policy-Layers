Task 6 – Install and Verify the Inline Layer

1\. Objective



The objective was to install the Orion-Layers policy package and verify the enforcement of the DMZ-Policy Inline Layer through network traffic testing.



2\. Installation Status



Policy installation could not be completed because a functional Security Gateway appliance was unavailable.



The environment reported a TCP connectivity failure during the installation attempt.



3\. Traffic Test Results



The following tests were not performed:



Test	Traffic Description	Actual Result	Matching Layer/Rule

T6	Internal host accessing Web\_Server using HTTP	Not Performed	Not Available

T7	Internal host accessing Mail\_Server using SMTP (TCP 25)	Not Performed	Not Available

T8	Internal host accessing Web\_Server using Telnet (TCP 23)	Not Performed	Not Available

T9	Internal host accessing external server using HTTP	Not Performed	Not Available

4\. Expected Policy Behavior



Based on the configured DMZ-Policy rules:



T6 should match the Web Access rule and be permitted, subject to the remaining applicable Ordered Layers.

T7 should match the Mail Access rule and be permitted, subject to the remaining applicable Ordered Layers.

T8 should not match either the Web Access or Mail Access rule and should reach the DMZ-Policy Cleanup Rule if it matches the parent Internal to DMZ rule.

T9 does not match the Internal to DMZ parent rule and is evaluated through the applicable Ordered Layers.



These are expected policy outcomes, not observed traffic results.



5\. T5 and T8 Comparison



T5 and T8 both involve Telnet traffic to Web\_Server.



Before the Inline Layer was attached, the Network layer's Internal to DMZ rule permitted the traffic to continue to Service-Control. Since Telnet was not included in the permitted services, the Service-Control Cleanup Rule was expected to drop it.



After the DMZ-Policy Inline Layer was attached, traffic matching the Internal to DMZ parent rule was additionally inspected by DMZ-Policy.



Telnet does not match the Web Access or Mail Access rules, so the DMZ-Policy Cleanup Rule is expected to drop it.



Therefore, the expected enforcement point changes from the Service-Control Cleanup Rule to the DMZ-Policy Cleanup Rule.



The comparison could not be confirmed using actual gateway logs because installation and traffic testing were unavailable.



6\. Conclusion



The DMZ-Policy Inline Layer was successfully configured in SmartConsole. However, its runtime enforcement and the T5/T8 log comparison remain unverified because a functional Security Gateway appliance was unavailable.

