# Web Expansion: Phishing QR & IDOR Exploitation

## Mission Description
This challenge simulated a Phishing and Bank Fraud incident. The threat actors created a fake banking application and distributed a malicious QR code to trick victims into submitting their credit card details (bypassing 3D Secure flows). The objective was to safely analyze the QR code payload, investigate the attacker's infrastructure, and retrieve the hidden flag.

## Tools & Environment
*   **QR Decoding:** Web-based utilities (for URL extraction without direct execution/scanning).
*   **OSINT / Malware Analysis:** urlscan.io (for passive infrastructure investigation).
*   **Isolated Sandbox:** Google Cloud Shell.
*   **CLI Utilities:** `curl` (for querying and analyzing HTML source code directly in the terminal).

## Methodology

### 1. OPSEC and Safe Decoding
To avoid exposing personal network data or risking malware execution on a mobile device, I refused to scan the QR code directly with my phone. Instead, I uploaded the image to a web-based decoding site to extract only the text string. This revealed a suspicious URL.

### 2. Passive Infrastructure Analysis
I submitted the extracted URL into urlscan.io for passive analysis. The results exposed the attacker's server IP address and a web directory containing 4 to 5 files, one of which appeared highly suspicious.

### 3. Web Expansion in Cloud Shell
To actively interact with the infrastructure without compromising my local machine, I launched an isolated environment in Google Cloud Shell. I utilized the `curl` command to download and inspect the source code:

```bash
curl -s -L "http://[ATTACKER_IP]/suspicious_file.html"
```
By analyzing the HTML/JS returned in the terminal, I discovered a hidden file that required administrator permissions, accessible via a specific URL parameter.

### 4. Vulnerability Exploitation (IDOR)
Access to the resources was controlled by a sequential parameter (bash=B3). I deduced that the infrastructure was vulnerable to Insecure Direct Object Reference (IDOR) and began manually iterating through the possible parameter values:
```bash
curl -s "http://[ATTACKER_IP]/admin_panel?bash=B4"
curl -s "http://[ATTACKER_IP]/admin_panel?bash=B3"
curl -s "http://[ATTACKER_IP]/admin_panel?bash=B1"
```
Upon reaching the beginning of the logical sequence (B0), I extracted the code block containing the flag:
```bash
curl -s "http://[ATTACKER_IP]/admin_panel?bash=B0" | grep "CTF"
```
### 5. Remediation & Security Recommendations
The critical flaw made by the threat actors was the implementation of sequential and predictable identifiers (B0, B1). To remediate this vulnerability, developers should:

Use Unpredictable Identifiers: Implement UUIDs (Universally Unique Identifiers) or randomized cryptographic tokens instead of sequential IDs.

Enforce Authorization Validation: Implement strict server-side access control matrix checks to ensure the user is genuinely authorized to view the requested resource.
