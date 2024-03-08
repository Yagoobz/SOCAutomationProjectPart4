<h2>SOC Automation Lab Part 4</h2>

<h3>Objectives</h3>
- ... 
<br />
<br />

In the Windows 10 machine, I navigate to the "ossec-agent" folder in Program Files (x86) and locate the "ossec.conf" file that requires editing. As a precaution, I create a backup copy of the file. Next, I open Notepad with administrative privileges and proceed to make changes in the "ossec.conf" file. Firstly, I find the full name of the Sysmon configuration file in the Windows Event Viewer and replace the "application" name in the "location" section of the "ossec.conf" file with it. Then, I remove the "security" and "system" events to prevent them from forwarding to our Wazuh manager. After completing these modifications, I restart Wazuh from Windows Services to ensure the changes take effect.
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/501a5f67-f214-46b3-afb3-18773cbea606" height="30%" width="70%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/b1072f53-b18d-4881-89cc-be5befc6ada6" height="30%" width="70%" alt="Disk Sanitization Steps"/>
