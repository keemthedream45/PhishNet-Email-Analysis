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
- AI tools (chatGPT) - to quickly decode the Base64 block
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

--

My third and fourth questions were: "What is the sender's email address?" and "What is the 'Reply-To' email address specified in the email?"
By examining the body of the email, I found the sender’s email listed at the top and the “Reply-To” address near the bottom. The two addresses were different, which is a major red flag indicating a potential spoofing or phishing attempt.
<img width="804" height="377" alt="Screenshot From 2025-10-31 02-48-08" src="https://github.com/user-attachments/assets/8051aa0b-4d07-4580-8ea8-3c5e98be5db5" />
<img width="1149" height="1150" alt="Screenshot From 2025-10-31 02-56-21" src="https://github.com/user-attachments/assets/00821b58-4945-456e-995e-5141f4f67ece" />

--

The next questions were: "What is the SPF (Sender Policy Framework) result for this email?", "What is the domain used in the phishing URL inside the email?", and "What is the fake company name used in the email?"
Since the email appeared legitimate, it was likely not flagged as spam. The SPF result, found in the [Received-SPF:] header, showed a pass. For the remaining two questions, I examined the body of the email, where I identified both the phishing domain used in the malicious link and the fake company name presented in the message.
<img width="804" height="377" alt="Screenshot From 2025-10-31 02-48-08" src="https://github.com/user-attachments/assets/3d4723d4-1328-492e-b3db-4f07ed3f851b" />
<img width="1149" height="1150" alt="Screenshot From 2025-10-31 02-56-21" src="https://github.com/user-attachments/assets/589d53a7-3f5e-49c6-ae08-7505439f4e85" />

--

My final three questions were: "What is the SHA-256 hash of the attachment?", "What is the filename of the malicious file contained within the ZIP attachment?", and "Which MITRE ATT&CK techniques are associated with this attack?"
To determine the hash, I used an AI tool to decode the Base64 string found at the bottom of the email footer into hex, which revealed details such as the decoded blob length, ZIP file header, and the malicious file name. For the last question, I concluded that the attack aligned with the MITRE ATT&CK technique T1566.001 — Spearphishing Attachment, where an adversary delivers a malicious ZIP attachment containing malware to compromise the target system.
<img width="643" height="560" alt="Screenshot From 2025-10-31 15-27-55" src="https://github.com/user-attachments/assets/54e839af-f7bd-4134-a183-e6bf9930f820" />
<img width="1153" height="1094" alt="Screenshot From 2025-10-31 15-28-37" src="https://github.com/user-attachments/assets/aad72a5b-061f-4de1-bf29-c2306f325c90" />


-- Link To Lab (https://labs.hackthebox.com/achievement/sherlock/2520523/985)
