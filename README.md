# cyber-security-tast3
OBJECTIVE : Use free tools to identify common vulnerabilities on your computer

Vulnerability Assessment Report – Nessus Essentials Scan

A vulnerability assessment was conducted to identify potential weaknesses on a single target system using Tenable Nessus Essentials, a widely recognized vulnerability scanning tool. The goal of this exercise was to evaluate the security posture of the target, determine whether any known vulnerabilities or misconfigurations were present, and understand how the scanning configuration affected the results.

The assessment focused on the use of free and open-source tools for vulnerability discovery and was complemented by additional security checks using utilities such as Nmap and Lynis. The purpose of this report is to summarize the Nessus scan configuration, interpret the findings, explain possible limitations of the scan, and recommend concrete remediation steps to improve system security.

 2 Scan Configuration Overview

The Nessus scan was performed using Nessus Essentials version 10.10.0 (build 20152) on a Linux-based scanner (ubuntu1604-x86-64). The selected scan policy was Basic Network Scan, which focuses primarily on discovering open ports and identifying services running on the target host.

Below is a summary of the key configuration parameters visible in the captured Nessus output:

Parameter	Value
Nessus Version	10.10.0
Scanner OS	Ubuntu 16.04 x86-64
Scan Type	Normal (Network Scan)
Scan Policy	Basic Network Scan
Scanner IP	192.168.128.135
Port Scanner	nessus_syn_scanner
Scan for Unpatched Vulnerabilities	Disabled
Web Application Tests	Disabled
Safe Checks	Enabled
Credentialed Checks	None
Max Hosts	30
Max Checks	4
Plugin Supersedence Plugin	Failed to launch
Report Verbosity	1 (low)

The scan was executed on a single target within the local network (192.168.128.135) with default settings. No authentication credentials were supplied, and intrusive plugin families were disabled.

3. Observations and Findings

The output visible in the screenshot contains scan metadata only, not the actual vulnerability results. This suggests that either:

No significant vulnerabilities were discovered; or

The scanning configuration prevented Nessus from performing deeper checks.

Based on the configuration parameters, several limitations can be identified that likely contributed to a lack of findings:

Credentialed Scanning Disabled: Without credentials, Nessus cannot log into the target to verify patch levels, local misconfigurations, or insecure system settings. This leads to incomplete results.

Unpatched Vulnerability Checks Disabled: The scan did not attempt to match detected service versions to known Common Vulnerabilities and Exposures (CVEs). This means critical security gaps could remain undiscovered.

Web Application Tests Disabled: If the target hosts any web applications, Nessus did not evaluate them for vulnerabilities such as SQL injection, cross-site scripting (XSS), or outdated CMS components.

Safe Checks Enabled: Although this minimizes the risk of service disruption, it limits the aggressiveness of the scan and reduces vulnerability coverage.

Plugin Supersedence Error: A plugin loading issue was reported (“plugin did not launch”), which may indicate incomplete or outdated plugin feeds, further reducing the effectiveness of the scan.

Low Parallelism: With “Max checks” limited to four, scanning speed and completeness were constrained, and certain plugins may have timed out before completion.

Because of these restrictions, the scan effectively functioned as a light reconnaissance scan rather than a comprehensive vulnerability assessment.


Analysis of Results

Even though the scan produced limited findings, the configuration details provide valuable insights into the security assessment process:

The Basic Network Scan successfully enumerates reachable hosts and detects open ports This information alone can help network administrators verify exposure and identify unauthorized or unnecessary services.

However, the absence of unpatched vulnerability detection and credentialed checks means the scan missed deeper OS- and application-level weaknesses.

Since Nessus Essentials relies on updated plugin feeds to detect CVEs, the plugin supersedence error should be corrected by updating the feed and restarting the Nessus service.

The configuration also shows that the scanner itself is running on an older platform (Ubuntu 16.04), which has reached end of life. Using an unsupported OS for security scanning introduces potential risk if the scanner host is not properly maintained.
