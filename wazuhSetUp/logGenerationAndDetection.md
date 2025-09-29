<div align="center">
  
## LOG GENERATION & DETECTION

We have communication between agents and server - lets generate some actions and get the log(s) rolling!
<p align="center">
  <img src="https://media1.tenor.com/m/8SwMrENO6AEAAAAC/pikachu-togepi.gif" width="300" alt="Pikachu Gif">
</p>

</div>
<div align="center">
  <h1> Part 1: Basic Log Generation </h1>
</div>

An easy one to start off with is an incorrect login from the physical device. Lets input the wrong password
about 10 times
<div align="center">
  <img width="882" height="192" alt="image" src="https://github.com/user-attachments/assets/0b45b0e8-c206-4d90-a432-b3893bc27afa" />
</div>

 **TO DO** 
 Insert a screenshot

Wazuh querying is great - it uses a pretty standard format. Having used ServiceNow querying and SQL language before its a breeze!
<div align="center">
  <img width="623" height="268" alt="image" src="https://github.com/user-attachments/assets/9c14c832-ffcb-423c-8c98-fdfde956e877" />
</div>

Now how about showing if someone was trying to access the device <i>internally</i>?  
On the agent machine I started an elevated PowerShell session and ran the *whoami* command.  
<p align="center">
  <img width="291" height="89" alt="image" src="https://github.com/user-attachments/assets/dc00a584-4d67-42ba-9981-665147e87493" />
</p>

On our dashboard we can see a new log was generated detailing the event. Device name,
IP, account name, channel used, and other important information can be found here in either
a table format or the JSON it's sent in.

Also provided is the MITRE techniques and tactics most associated with the log event. 
<p align="center">
  <img width="780" height="125" alt="image" src="https://github.com/user-attachments/assets/119c8b87-bbbb-471d-ac6b-c658a040c5b3" />  
</p>
It aligned perfectly as escalating to a local admin account gives attackers a better foothold to keep going up the chain. I'm just
glad it was a simple *whoami* command. You can read more about the technique [here](https://attack.mitre.org/techniques/T1078/).


<h1 align="center"> Part 2: A Slighly More Sophisticated Attack</h1>
Let's see if we can detect activity in the different stages of the <a href="https://attack.mitre.org/">Cyber Kill-Chain</a>
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/19fdf6c8-6beb-418f-9266-b5dbced142bd" />  
An attacker might start with a portscan as they begin their <b>reconaissance</b> to see any openings. To replicate this we will bootup a <b>Kali-Linux</b> instance
and use the <a href="https://nmap.org/">nmap</a> tool.  
<div align="center">
  <img width="569" height="340" alt="image" src="https://github.com/user-attachments/assets/a8b8a1dd-c84f-4c9c-ab8a-f63574a0cbbf" />
</div>
After allowing logging in Windows Defender Firewall (for all network profiles as this communication comes via internal network) I able to ensure
nmap connections (and all connections thereafter) were being logged via pfirewall.log. Now, in Agent 1's ossec config file I added pfirewall logs were to be directed at my manager. 
<a href="https://documentation.wazuh.com/current/user-manual/manager/event-logging.html">Enabling logging in my manager</a> showed that my manager was receiving the logs. Now, 
Wazuh demands we create a <a href="https://github.com/jacobbria/Homelab-SIEM.Hazah-Wazh/blob/main/sideQuests/makingWazuhRules.md">custom decoder and rule set</a>a for it to trigger alerts or show in the discover dashboard. 

<div class="align"> 
  <img width="1343" height="824" alt="image" src="https://github.com/user-attachments/assets/a9781246-9558-4399-a14d-cd382cf2ccb6" />
</div>

Within Wazuh pings will now trigger an alert inside my Snort NIDS and then sent to my Wazuh Manager. It will show up as an "IDS Event" which is generic and can later be clarified but fulfils the goal of this 
project.
<div align="center">
  <img width="1191" height="141" alt="image" src="https://github.com/user-attachments/assets/3682d2f5-93b2-4a63-8183-b303d8cdf7fe" />
</div>

