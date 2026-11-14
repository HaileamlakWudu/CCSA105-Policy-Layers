# Task 6 – Install and Verify the Inline Layer

## 1. Objective

The objective of this task was to install the `Orion-Layers` policy package on the cloud Security Gateway and verify the enforcement of the `DMZ-Policy` Inline Layer through network traffic testing.

The testing focused on verifying whether traffic matching the parent `Internal to DMZ` rule was inspected by the Inline Layer and handled according to its configured rules.

## 2. Installation Status

The `DMZ-Policy` Inline Layer was already configured and attached to the `Internal to DMZ` rule in the `Network` layer.

The Inline Layer contained the following rules:

1. **Web Access** – controls permitted web traffic to the Web Server.
2. **Mail Access** – controls permitted SMTP traffic to the Mail Server.
3. **Cleanup Rule** – drops traffic that does not match the permitted rules.

The updated `Orion-Layers` policy package was successfully published and installed on the cloud Security Gateway.

**Installation result:** Successful.

This confirmed that the updated policy package, including the Inline Layer configuration, was installed on the cloud Security Gateway. However, successful installation alone does not establish that the Inline Layer correctly handled individual traffic tests.

## 3. Traffic Test Results

The following table records the current test results.

| Test | Traffic Description | Actual Result | Matching Layer/Rule |
|---|---|---|---|
| T6 | Internal host accessing Web_Server using HTTP (TCP 80) | Failed – connection timed out; no corresponding firewall log found | Not verified |
| T7 | Internal host accessing Mail_Server using SMTP (TCP 25) | Not yet tested | Not available |
| T8 | Internal host accessing Web_Server using Telnet (TCP 23) | Not yet tested | Not available |
| T9 | Internal host accessing external server using HTTP | Not yet tested | Not available |

### T6 – HTTP Access to Web_Server

**Test configuration:**

- Source: Cloud lab Windows workstation
- Destination: `Web_Server` – `172.16.10.20`
- Service: HTTP (TCP/80)

**Command executed:**

```powershell
curl.exe -v --connect-timeout 5 http://172.16.10.20/
```

**Actual output:**

```text
* Trying 172.16.10.20:80...
* Connection timed out after 5011 milliseconds
* closing connection #0
curl: (28) Connection timed out after 5011 milliseconds
```

**Observation:**

The connection attempt to the Web Server timed out after approximately five seconds. The HTTP request did not receive a response.

A corresponding traffic entry could not be found in SmartConsole Logs & Monitor. Therefore, the exact enforcement point and matching firewall rule could not be established.

**T6 conclusion:**

T6 was attempted, but successful HTTP connectivity and enforcement by the `DMZ-Policy` Inline Layer could not be verified. A timeout without a corresponding firewall log does not establish whether the traffic was blocked by the firewall, affected by a routing or connectivity issue, or unanswered by the destination server.

**Evidence:**

- `T6-01-Inline-Policy-Installation.png` – successful policy installation.
- `T6-02-Web-Server-HTTP-Test.png` – terminal output showing the HTTP connection timeout.

## 4. Expected Policy Behavior

Based on the configured `DMZ-Policy` Inline Layer rules, the expected behavior is as follows.

### T6 – HTTP to Web_Server

Traffic from an internal host to `Web_Server` using HTTP should match the `Web Access` rule in the `DMZ-Policy` Inline Layer and be accepted, subject to the remaining applicable Ordered Layers.

This expected behavior was not confirmed by the actual test because the connection timed out and no corresponding firewall log was found.

### T7 – SMTP to Mail_Server

Traffic from an internal host to `Mail_Server` using SMTP (TCP/25) should match the `Mail Access` rule in the `DMZ-Policy` Inline Layer and be accepted, subject to the remaining applicable Ordered Layers.

This test has not yet been performed.

### T8 – Telnet to Web_Server

Traffic from an internal host to `Web_Server` using Telnet (TCP/23) should match the parent `Internal to DMZ` rule and enter the `DMZ-Policy` Inline Layer.

Since Telnet is not included in either the `Web Access` or `Mail Access` rule, it should reach the Inline Layer's `Cleanup Rule` and be dropped.

This test has not yet been performed.

### T9 – HTTP to External Server

Traffic from an internal host to an external server using HTTP does not match the parent `Internal to DMZ` rule because its destination is outside the DMZ network.

Therefore, it should not enter the `DMZ-Policy` Inline Layer through that parent rule. Instead, it should be evaluated by the applicable Ordered Layers and their configured rules.

This test has not yet been performed.

The above descriptions are expected policy outcomes based on the configuration. They must not be interpreted as observed traffic results.

## 5. T5 and T8 Comparison

T5 and T8 both involve Telnet traffic from an internal host to `Web_Server` using TCP port 23.

The difference is the policy structure in place when each test is performed.

### T5 – Before the Inline Layer

During Task 4, before the `DMZ-Policy` Inline Layer was attached, Telnet traffic to `Web_Server` was expected to match the parent `Internal to DMZ` rule in the `Network` layer.

The traffic would then continue to the `Service-Control` layer. Since Telnet was not included in the permitted services, it was expected to reach the `Service-Control` Cleanup Rule and be dropped.

The actual T5 result must be taken from the Task 4 firewall logs. The expected behavior alone does not confirm that the test was successfully performed.

### T8 – After the Inline Layer

After the `DMZ-Policy` Inline Layer was attached, Telnet traffic matching the parent `Internal to DMZ` rule was additionally evaluated by the Inline Layer.

Telnet does not match either the `Web Access` or `Mail Access` rule. Therefore, it is expected to reach the `DMZ-Policy` Cleanup Rule and be dropped.

T8 has not yet been performed, so this expected enforcement point has not been confirmed using actual gateway logs.

### Comparison

| Item | T5 – Before Inline Layer | T8 – After Inline Layer |
|---|---|---|
| Destination | Web_Server | Web_Server |
| Service | Telnet (TCP/23) | Telnet (TCP/23) |
| Parent rule | Internal to DMZ | Internal to DMZ |
| Expected enforcement point | Service-Control Cleanup Rule | DMZ-Policy Cleanup Rule |
| Actual verification | Refer to Task 4 logs | Not yet tested |

The expected difference is that Telnet traffic is handled by the `Service-Control` Cleanup Rule before the Inline Layer is introduced, whereas after the Inline Layer is attached, it should be handled by the `DMZ-Policy` Cleanup Rule.

The comparison remains unverified until the relevant T5 and T8 firewall log entries are available.

## 6. Evidence

The following evidence is associated with Task 6:

| Evidence File | Description | Status |
|---|---|---|
| `T6-01-Inline-Policy-Installation.png` | Successful installation of the updated Orion-Layers policy package | Collected |
| `T6-02-Web-Server-HTTP-Test.png` | Windows terminal showing the HTTP connection timeout | Collected |
| `T6-03-Web-Server-HTTP-Log.png` | SmartConsole log evidence for T6, if a matching entry becomes available | Not available |


## 7. Conclusion

The `DMZ-Policy` Inline Layer was successfully configured, attached to the parent `Internal to DMZ` rule, and installed as part of the updated `Orion-Layers` policy package on the cloud Security Gateway.

Runtime verification was attempted for T6, which involved HTTP access to `Web_Server`. The connection timed out after approximately five seconds, and no corresponding firewall log was found. Therefore, the exact reason for the timeout and the Inline Layer's enforcement of this traffic could not be confirmed.

The expected policy behavior indicates that HTTP traffic should match the `Web Access` rule, SMTP traffic should match the `Mail Access` rule, and Telnet traffic should be dropped by the Inline Layer's Cleanup Rule. External HTTP traffic should be evaluated outside the Inline Layer through the applicable Ordered Layers.

T7, T8 and T9 have not yet been performed. The T5/T8 comparison also remains unverified until the relevant gateway logs are available.

Overall, policy installation was successful, but full runtime verification of the Inline Layer remains incomplete.
