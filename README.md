# PhishNet-Email-Analysis
An accounting team receives an urgent payment request from a known vendor. The email appears legitimate but contains a suspicious link and a .zip attachment hiding malware. Your task is to analyze the email headers, and uncover the attacker's scheme.

## Objective
This lab will develop my practical skills in email forensics and phishing detection. The primary focus is to analyze suspicious email headers, links, and attachments to identify indicators of compromise, trace the attacker’s origin, and understand how malware is delivered through social engineering tactics.

### Skills Learned
- Email Header Analysis – Learn how to trace the originating IP, mail relay servers, and spoofed sender details to identify signs of phishing or impersonation.
- Malware and Attachment Investigation – Gain hands-on experience inspecting ZIP attachments, calculating file hashes, and uncovering malicious payloads hidden within emails.
- Threat Intelligence & Detection Techniques – Strengthen your ability to identify phishing URLs, recognize social engineering indicators, and map findings to MITRE ATT&CK techniques for professional threat reporting.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used
- Isolated VM (Fedora) — run analysis safely, take snapshots.
- Text editor / pager (vim, less) — view raw email files and headers.
- unzip — inspect ZIP contents (inside VM).
- grep — parse headers quickly from raw email.
- nslookup — DNS lookups for domains and mail servers.
- whois — registrar/ownership info for suspicious domains.


## Steps
The first step that was asked is "What is the originating IP address of the sender?" To answer this question i first started with unziping the PhishNet.zip file Once the file was unzipped, I confirmed the extraction was successful by using the [ls] command to list the files in my Downloads directory, where a new file named email.eml appeared.
<img width="744" height="102" alt="Screenshot From 2025-10-31 01-00-14" src="https://github.com/user-attachments/assets/0a444549-178d-467f-900f-46ab318c7d01" />
<img width="752" height="184" alt="Screenshot From 2025-10-31 00-56-40" src="https://github.com/user-attachments/assets/bfb824ab-6fdb-4fd5-bc07-378e3d201a89" />
<img width="803" height="183" alt="Screenshot From 2025-10-31 01-03-25" src="https://github.com/user-attachments/assets/0024f236-f1d9-4e31-bd4d-e179ff1544ab" />
<img width="471" height="27" alt="Screenshot From 2025-10-31 01-14-17" src="https://github.com/user-attachments/assets/08dcd8ce-cde0-4f0c-95c6-a977f667c8e8" />
From there I used [less] to view the email headers; the X-Originating-IP field showed 45.67.89.10, which is the originating IP address.
<img width="892" height="644" alt="Screenshot From 2025-10-31 01-15-27" src="https://github.com/user-attachments/assets/167c6cbc-aab5-4af3-9d4a-4211b52a1c4d" />

--

My next question in the lab was, "Which mail server relayed this email before reaching the victim?" I inspected the Received header chain and identified the final mail server that relayed the message before delivery to be [203.0.113.25].
<img width="816" height="195" alt="Screenshot From 2025-10-31 02-20-04" src="https://github.com/user-attachments/assets/76a59bc9-5ede-43b2-82d1-8813888bfc88" />
<img width="1149" height="1150" alt="Screenshot From 2025-10-31 02-16-35" src="https://github.com/user-attachments/assets/1dd8c648-e54f-4af8-86f5-3eae38f44221" />

