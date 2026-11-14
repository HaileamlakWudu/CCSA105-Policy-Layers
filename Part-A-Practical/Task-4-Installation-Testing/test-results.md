# Task 4 – Policy Installation and Initial Connectivity Testing

## 1. Objective

The objective of this task was to install the `Orion-Layers` policy package on the cloud Security Gateway, test SSH connectivity from the administrator workstation, investigate the initial result, and verify the effect of the Ordered Layers on network traffic.

Testing was performed in the cloud lab because the home lab did not have a functional Security Gateway for runtime traffic testing.

## 2. Policy Installation

The `Orion-Layers` policy package was present in SmartConsole and had the following Ordered Layer structure:

1. `Network`
2. `Service-Control`

The `Service-Control` layer was positioned below the `Network` layer.

The policy package was successfully installed on the cloud Security Gateway during the earlier configuration work.

**Installation result:** Successful, based on the cloud-lab installation evidence.

## 3. Initial SSH Connectivity Test (T1)

### Test details

| Item | Value |
|---|---|
| Test ID | T1 |
| Source expected by policy | `Admin_PC` – 10.1.1.101 |
| Destination | Security Gateway |
| Service | SSH (TCP/22) |
| Expected policy rule | `Admin Access` in Network and `Admin Services` in Service-Control |
| Actual result | Failed – connection timed out |

### Observed result

An SSH connection was attempted from the cloud lab to the Security Gateway. The connection timed out.

The `Admin Services` rule was already present in the cloud-lab `Service-Control` layer. However, the source address observed by the gateway did not match the private IP address configured in the rule for `Admin_PC`.

The cloud connection was arriving with a public/NAT source IP rather than `10.1.1.101`. Consequently, the traffic did not match the source condition in the `Admin Services` rule.

The firewall logs showed the traffic being blocked by the applicable blocking rule. The attached log evidence should be used to identify the exact rule and layer associated with each logged attempt.

### Explanation

The `Admin Services` rule is configured to allow SSH and HTTPS from `Admin_PC` to the Security Gateway. However, a firewall rule only matches when the traffic satisfies its configured conditions, including the source address.

Since the source address observed by the gateway differed from the configured `Admin_PC` address, the rule did not match.

The following distinction is important:

- If the traffic is dropped by the `Stealth Rule` in the `Network` layer, evaluation stops at that rule.
- If the traffic passes the `Network` layer, it can continue to the `Service-Control` layer, where a non-matching service or source can eventually be dropped by the cleanup rule.

These are separate possible blocking points. The SmartConsole logs should determine which one applied to each connection attempt.

**Conclusion for T1:** SSH connectivity was unsuccessful because the source address observed by the cloud Security Gateway did not match the private source address configured in the policy. The existence of the `Admin Services` rule alone did not guarantee that the connection would be accepted.

## 4. Admin Services Rule Configuration

The cloud-lab `Service-Control` layer contained the following rule:

| Field | Configuration |
|---|---|
| Rule name | Admin Services |
| Source | Admin_PC |
| Destination | Security Gateway |
| Services | SSH, HTTPS |
| Action | Accept |
| Track | Log |
| Position | First rule |

The rule was already configured when the cloud SSH test was performed. Therefore, this cloud test was not a test of the policy before adding the rule; it was a test of the existing rule when the incoming source address did not match its configured source object.

## 5. T1–T5 Test Results

The following table records the results currently established. The remaining tests must be performed before this section can be considered complete.

| Test | Traffic | Result | Matching layer/rule or status |
|---|---|---|---|
| T1 | Admin_PC → Gateway, SSH | Failed – timeout | Source-address mismatch; use the log to confirm the exact blocking layer and rule |
| T2 | Another internal host → External server, HTTP | Not yet tested | Pending |
| T3 | Another internal host → External server, Ping | Not yet tested | Pending |
| T4 | Another internal host → Gateway internal interface, Ping | Not yet tested | Pending |
| T5 | Another internal host → Web_Server, Telnet TCP/23 | Not yet tested | Pending |

Do not report T2–T5 as successful or blocked until the tests have been performed and their corresponding logs have been reviewed.

## 6. Evidence

The following evidence will be attached to this task:

| Evidence file | Description |
|---|---|
| `T4-01-Policy-Installation.png` | Successful policy installation in the cloud lab |
| `T4-02-Admin-Services-Rule.png` | Admin Services rule in the Service-Control layer |
| `T4-03-SSH-Command-Attempt.png` | Terminal screenshot showing the SSH connection attempt and timeout |
| `T4-04-SSH-Firewall-Log.png` | SmartConsole log showing the SSH attempt, observed source address, action, layer and matching rule |

Additional evidence for T2–T5 will be added after those tests are completed.

## 7. Conclusion

The cloud lab allowed the policy package to be installed and runtime connectivity testing to begin. The SSH test did not succeed, even though the `Admin Services` rule was configured.

The investigation identified a source-address mismatch: the rule expects traffic from the private `Admin_PC` address, but the cloud Security Gateway sees the connection arriving from a public/NAT address. This prevents the traffic from matching the intended rule and allows a later blocking rule to handle it.

This result demonstrates why firewall policy testing must consider the actual source address observed by the gateway, not only the address configured on the administrator workstation.

The remaining T2–T5 tests and their corresponding firewall logs are required to complete the full Task 4 test matrix.
