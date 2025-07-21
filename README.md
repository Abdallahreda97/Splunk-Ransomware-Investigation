# 🔐 Ransomware Investigation using Splunk

## 📌 Overview
This project demonstrates a hands-on investigation of a simulated **Ransomware attack** using Splunk. The dataset contains suspicious logs related to PowerShell and registry modifications typically observed during a ransomware infection.

## 📂 Dataset Used
- **Source**: [Sysmon logs from Atomic Red Team - MITRE ATT&CK T1546.015](https://media.githubusercontent.com/media/splunk/attack_data/master/datasets/attack_techniques/T1546.015/atomic_red_team/windows-sysmon.log)
- **Index**: `ransomware`
- **Source file**: `ransomware.log`
- **Sourcetype**: `Ransomware`
- **Host**: `Elmohr`

---

## 🧪 Investigation Steps

### ✅ Step 1: Load the dataset into Splunk
I uploaded the `.log` file to Splunk via:
Settings → Add Data → Upload → Select ransomware.log → Choose index=ransomware


---

### ✅ Step 2: Explore raw event logs
**Query**:
`spl
index=ransomware source="ransomware.log" host="Elmohr"
| table _time, host, EventCode, Image, CommandLine, ParentImage, User
| sort _time. 
Purpose: To get an overview of the commands and see anything abnormal like PowerShell or reg.exe usage.


✅ Step 3: Identify suspicious behavior
Looked for:

Use of PowerShell with base64-encoded commands

Registry edits using reg.exe

Shadow copies deletion using vssadmin

Unusual ParentImage values (e.g., PowerShell spawning reg.exe)

✅ Step 4: Extract key fields (Field Extraction)
Manually extracted fields from _raw if needed, especially for identifying:

CommandLine actions

Parent/Child process relationships

Targeted registry keys

✅ Step 5: Build a Timeline

spl

index="ransomware"
| stats count by _time, CommandLine
| sort _time
Visualized the attack sequence using Timeline view to see when the commands were executed.


✅ Step 6: Use Visualizations
Timeline Chart: Showed command execution peaks

Bar Chart: Showed most used tools (e.g., PowerShell, reg.exe)


🔍 Sample Screenshots
✅ Timeline of attack sequence

✅ Raw log inspection with suspicious PowerShell

✅ Visualization of CommandLine activity

✅ Extracted fields and decoded base64 commands

(Insert screenshots here)

🧾 Conclusion
Through this Splunk-based investigation, I was able to:

Detect suspicious PowerShell usage

Uncover registry edits pointing to persistence

Build a clear timeline of the ransomware attack

Practice field extraction and data visualization

🛡️ Tools & Skills Used
Splunk Search & Reporting

Field Extraction

Sysmon log analysis

MITRE ATT&CK techniques

Cybersecurity Blue Team analysis




