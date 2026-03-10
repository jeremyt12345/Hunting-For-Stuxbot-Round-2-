# Hunting-For-Stuxbot-Round-2-


Part two 

Q1 "Create a KQL query to hunt for "Lateral Tool Transfer" to C:\Users\Public. Enter the content of the user.name field in the document that is related to a transferred tool that starts with "r" as your answer."

The objective was to identify a tool transferred to C:\Users\Public and find the associated user account.
Since a file transfer means something was written to disk, I used Sysmon Event ID 11 (FileCreate) with the following query: "event.code:11 AND file.path:*Public*"

This returned results showing a file named Rubeus.exe dropped to C:\Users\Public on March 27, 2023 at 17:54. Expanding the event revealed the user.name field which identified the account responsible for the transfer.


<img width="1847" height="571" alt="image" src="https://github.com/user-attachments/assets/11e443ab-f18c-4f6b-98d0-94a6dc90b58d" />


Q2 "Create a KQL query to hunt for "Boot or Logon Autostart Execution: Registry Run Keys / Startup Folder". Enter the content of the registry.value field in the document that is related to the first registry-based persistence action as your answer."

Thinking through this one my first thought is that I should look through the event ID's and check which ones would require something starting or being set so that would be Event ID 13(Registry Value Set).
