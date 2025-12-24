# Website-Cloning-SMB-Enumeration
To demonstrate how attackers clone legitimate websites to harvest credentials using the Social-Engineer Toolkit (SET) and how a simple HTML redirect can be used as a phishing vector.
I elevated to root privileges and launched the Social-Engineer Toolkit.


sudo su
setoolkit
I navigated through the menu to select the Site Cloner method:
<img width="610" height="584" alt="image" src="https://github.com/user-attachments/assets/ce059435-8dcc-44b6-a479-eb67931c6bac" />

Selected 1 (Social-Engineering Attacks)
Selected 2 (Website Attack Vectors)
Selected 3 (Credential Harvester Attack Method)
Selected 2 (Site Cloner)
Step B: Configuration
IP address for the POST back: 10.6.6.1 (This tells the tool to send stolen credentials to my machine)
URL to clone: http://dvwa.vm (This is the legitimate login page being copied)<img width="806" height="589" alt="image" src="https://github.com/user-attachments/assets/ef3df808-21e0-405c-ad74-3c486d09202a" />



Step C: Creating the Phishing Trigger (The "Bait")
To simulate a victim clicking a malicious link, I created a local HTML file that automatically redirects the browser to my cloned site.

Opened a text editor.
Typed the following code:
HTML

<html>
<head>
<meta http-equiv="refresh" content="0; url=http://10.6.6.1/" />
</head>
</html>
Saved the file as ladies.html on the Desktop.
Step D: Execution
I double-clicked ladies.html.
The browser immediately redirected to 10.6.6.1, displaying the cloned DVWA login page.
I entered the following dummy credentials:
Username: ladies@gmail.com
Password: 1234
<img width="730" height="509" alt="image" src="https://github.com/user-attachments/assets/205b1f87-529d-4a01-833f-37e598268d9c" />

<img width="926" height="416" alt="image" src="https://github.com/user-attachments/assets/0590fec5-940b-4d58-a891-130fd11bfce6" />


Step E: Retrieving the Report
After the credentials were submitted, I returned to the terminal.
<img width="557" height="331" alt="image" src="https://github.com/user-attachments/assets/b93eebdb-084b-4fe1-a398-eabda57b4efb" />

Pressed Ctrl + c to stop the listener.
Typed 99 repeatedly to exit the toolkit menus.
Located and displayed the XML report containing the captured data:
Bash

cat /root/.set/reports/”2025-12-14 13:34:09.326665.xml”




Lab 2: SMB Vulnerability Scanning
1. Objective
To enumerate a target system via the Server Message Block (SMB) protocol to discover users, shares, and potential vulnerabilities using enum4linux.

2. Tools Used
OS: Kali Linux
Tool: enum4linux
Target: Metasploitable 2 (IP: 172.17.0.6)
3. Execution & Commands
I used the -a flag (Do All) to perform a comprehensive scan of the target.
<img width="842" height="600" alt="image" src="https://github.com/user-attachments/assets/4376c3fa-b152-45b1-a18f-24cee40249db" />
<img width="842" height="600" alt="image" src="https://github.com/user-attachments/assets/0ae13625-4476-440c-a168-98c4e4ad3575" />

Bash

# Syntax: enum4linux -a 172.17.0.6
enum4linux -a 172.17.0.6
