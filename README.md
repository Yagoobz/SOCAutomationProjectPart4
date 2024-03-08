<h2>SOC Automation Project Part 4</h2>

<h3>Objectives</h3>
- Generate Telemetry
<br />
- Ingest into Wazuh 
<br />
<br />

In the Windows 10 machine, I navigate to the "ossec-agent" folder in Program Files (x86) and locate the "ossec.conf" file that requires editing. As a precaution, I create a backup copy of the file. Next, I open Notepad with administrative privileges and proceed to make changes in the "ossec.conf" file. Firstly, I find the full name of the Sysmon configuration file in the Windows Event Viewer and replace the "application" name in the "location" section of the "ossec.conf" file with it. Then, I remove the "security" and "system" events to prevent them from forwarding to our Wazuh manager. After completing these modifications, I restart Wazuh from Windows Services to ensure the changes take effect. As an added bonus, I also receive the classic "Active Windows" alert on my Windows machine. :(
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/501a5f67-f214-46b3-afb3-18773cbea606" height="30%" width="70%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/b1072f53-b18d-4881-89cc-be5befc6ada6" height="30%" width="70%" alt="Disk Sanitization Steps"/>

Before downloading Mimikatz onto the machine, I must exclude the downloads path to prevent Windows from denying the download. Additionally, since Google Chrome might block the download, I adjust a setting to allow it. Once the download is complete, I open an administrative Windows PowerShell, navigate to the Mimikatz directory, and execute it.
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/0c616ea7-5165-4815-93b9-3c3960c22ecb" height="30%" width="70%" alt="Disk Sanitization Steps"/>

Before checking the Wazuh dashboard, I make adjustments in the "ossec.conf" file. Using "nano," I modify the "logall" and "logall_json" settings from "no" to "yes," then restart the Wazuh manager. This action initiates the archiving of all logs into a file named "archives," which will be located in "/var/ossec/logs/archives/." To enable Wazuh to ingest these logs, I update the configuration in Filebeat by editing the "filebeat.yml" file with "nano /etc/filebeat/filebeat.yml." Within this file, I set "archives enabled" to true and restart the Filebeat service.
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/d53af3e0-f197-44ce-ba57-9381b7fb31f7" height="30%" width="70%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/06ed39f1-d502-4632-8f16-55b001b46dc1" height="30%" width="70%" alt="Disk Sanitization Steps"/>

In the Wazuh manager, I create a new index specifically for archives, enabling me to search through all the logs seamlessly. And just like that, it's done!
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/9b09d5da-b391-4e6d-b836-2eca0c8b3c81" height="30%" width="70%" alt="Disk Sanitization Steps"/>

Before checking my Wazuh dashboard, I decide to double-check whether Mimikatz is being recognized. I generate another instance of Mimikatz in Windows PowerShell, and upon inspection of the event viewer, I confirm its presence. Additionally, I search for "Mimikatz" in the Wazuh manager using "grep." With everything in place, I proceed to the Wazuh dashboard, and sure enough, there it is!
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/eb415ff6-892c-42bc-85a5-f218979c27c6" height="30%" width="70%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/21f7a4d3-31b2-4eca-80c9-425a79e9a2fd" height="30%" width="70%" alt="Disk Sanitization Steps"/>
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/f56d4506-c47d-45de-8930-dcc0b7115284" height="30%" width="70%" alt="Disk Sanitization Steps"/>

In the Wazuh dashboard, I navigate to "manage rules" and select the "0800-sysmon_id_1.xml" file to create a custom rule for detecting Mimikatz. After copying a rule, I move to "custom rules" and access the "local_rules.xml" file. I paste the copied rule, adjusting the "rule id" to 100002 to avoid duplication, and set the severity level to the maximum value of 15. Then, I modify the "field name" to the original file name, change the "type" to "mimikatz," and update the "description" to "Mimikatz Usage Detected."
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/c777e160-92bd-444f-8d0d-03a73e19985b" height="30%" width="70%" alt="Disk Sanitization Steps"/>

Back in Windows PowerShell, I trigger another Mimikatz instance to test whether we receive an alert on the Wazuh dashboard. Lo and behold, the alert appears! We're all set!
<br />
<br />
<img src="https://github.com/Yagoobz/SOCAutomationLabPart4/assets/145611184/13c645f3-a50a-4d8c-b337-6ecac75a906c" height="30%" width="70%" alt="Disk Sanitization Steps"/>


