# Lab Environment Limitation and Resolution

## Home Lab Limitation

During the initial home-lab work, SmartConsole was connected to the Security Management Server, but a functional Security Gateway was not available for runtime testing.

Policy installation encountered a TCP connectivity failure. As a result, gateway-dependent activities such as SSH, HTTP, ICMP and Telnet testing, firewall log verification, and runtime policy enforcement could not be completed in that environment.

The policy configuration work was retained as evidence of the completed SmartConsole configuration.

## Cloud Lab Resolution

A cloud lab with a functional Security Gateway subsequently became available. The `Orion-Layers` policy package was successfully installed in the cloud environment.

This resolved the original gateway-availability limitation for policy installation and runtime testing.

The initial SSH test was attempted in the cloud lab but timed out. Investigation indicated that the source IP observed by the gateway was a public/NAT address rather than the private `Admin_PC` address configured in the `Admin Services` rule.

Therefore, the cloud environment enabled runtime testing, but the SSH test exposed a source-address matching issue that must be considered when interpreting the firewall logs.

## Current Status

- Home-lab policy configuration: Completed.
- Cloud-lab policy configuration: Completed.
- Cloud policy installation: Successful.
- Cloud SSH test (T1): Attempted; connection timed out due to a source-address mismatch indicated by the available observations.
- Cloud tests T2–T5: Pending completion and evidence collection.

The home-lab limitation remains relevant as a description of the original environment, but it no longer prevents the assignment's gateway-dependent testing from being carried out in the cloud lab.
