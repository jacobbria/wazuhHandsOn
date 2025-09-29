The logs seen in the _Discover_ and _Events_ tabs are only those that trigger a specific rule. Wazuh's out-of-the-box (OOTB) rules are very good. However, my desire to try and get notified anytime recon is done to my network lead me
down the path of making <a href="https://documentation.wazuh.com/current/user-manual/ruleset/rules/custom.html">custom rules</a>. 

This <a href="https://www.youtube.com/watch?v=nSOqU1iX5oQ">video</a> by John Hammond was super helpful. While previously I had commented on the great docs presented by Wazuh, I found this area needed some more clarification. 
Following along Hammond's video I was able to create custom rules after installing and configuring Sysmon unto Agent 1.

Wazuh rules can, easily enough, be managed in the _Rules_ tab on the browser dashboard. They follow XML format: 

<div align="center">
  <img width="504" height="188" alt="image" src="https://github.com/user-attachments/assets/4696bdc3-bd20-477e-871d-82cf5af07851" />
</div>

One area that the docs lack an emphasis on which gave me trouble until finding Hammonds video was the _if_sif__ tag. This tag basicaly connects or maps logs until an event type.

We now need to make a rule which would do the same but for recon.  
We will be port scanning Agent 1 using Kali hosted on a VM inside Agent 2. We will use the "noisest" scan available - nmap -A. Initially, I had set up Windows Defender Firewall
to log all connections and planned to create a rule based around noticing _x__ amount of dropped conncections over _x_ amount of time. After reading a really informative <a href="http://blog.bonsaiviking.com/2015/07/they-see-me-scannin-they-hatin.html">article</a> 
by Nmap dev Daniel Miller where he mentions the distinct signatures and artifacts left over by an nmap, I redrew my plans. Miller states about Nmap packets

<p>
  <i>
  "...these packets are unique, they can be detected easily. Some specific examples:
ICMP Echo Request with no payload. Snort IDS recognizes this with SID 469'"
  </i>
</p>

With that something came to mind.

<h1 align="center">
  Oink Oink - A New Plan Emerges
</h1>
<div align="center">
  <img width="1352" height="742" alt="image" src="https://github.com/user-attachments/assets/8b3f7ba0-1aad-4672-ab18-c3b76e4d1e98" />
</div>
New plan: use Snort as an IDS for Agent 1. With already recognized SIDs its either possible to create a new rule in Wazuh or, possibly, already existing configurations exist like with <a href="https://wazuh.com/resources/blog/emulation-of-attack-techniques-and-detection-with-wazuh/sysmonconfig.xml">Sysmon</a>
I document my time getting snort ready <a href="">here</a>. Snort is now sending logged alerts to Wazuh as confirmed by checking the archives on the manager. Luckily, Wazuh supports Snort already
with their alerts coming up as "IDS Event" so the need for further custom rules isnt needed.
