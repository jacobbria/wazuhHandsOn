&emsp;Wazuh provides some great resources for installing their system. Following that provided a mostly smooth process.
However, I was having some issues related to getting the server installed on the Ubuntu VM. It took about 3-4 attempts 
where I would install and recieve an error. Looking into the error logs wasn't too helpful but it was able to work after
giving the VM about 20GB more disk space.
<div align="center">
  
  ## Initial Set-up
  
<table>
<tr>
  <td>
<div align="center">
<h2>Wazuh Server </h2>
</div>
    
| *Component*       | Specification |
|-------------------|---------------|
| *Operating System*| Ubuntu        |
| *Disk (Storage)*  | 50 GB         |
| *RAM*             | 8 GB          |
| *Virtualization*  | VirtualBox    |
  
  </td>
<td>
  <div align="center">
  <h2>Wazuh Agent 1</h2>
  </div>
  
  | *Component*       | Specification |
  |-------------------|---------------|
  | *Operating System*| Windows 11    |
  | *Disk (Storage)*  | 1 TB          |
  | *RAM*             | 16 GB         |
  | *Virtualization*  | None    |

  </td>
  <td>
  <div align="center">
  <h2>Wazuh Agent 2</h2>
  </div>
  
  | *Component*       | Specification |
  |-------------------|---------------|
  | *Operating System*| Windows 11    |
  | *Disk (Storage)*  | 1 TB          |
  | *RAM*             | 16 GB         |
  | *Virtualization*  | None    |

  </td>
</tr>
</table>
</div> 

&emsp;The agent installation went great. Wazuh provides an easy process. I did have to did into the ossec config files 
to ensure my agent knew where to point. I was using different networks during this process so the machines were assigned 
various IPS.

&emsp;When doing this sort of project it helped to have DNS knowledge. VirtuaBox defaults its machines to using NAT - this 
prevents bidirectional communication between host and VM. Instead, using a bridged adapter allows the VM to be treated
as its own device and assigned an IP. After using some netstat tools to ping and tracert packets between my laptop
and VM, I was able to get the agent and VM talking.
<div align="center">

| Resources Used |
|----------|
| [Wazuh Documentation](https://documentation.wazuh.com/current/quickstart.html) |
| [Setup Your Own FREE SIEM at Home! - Wazuh (YouTube)](https://youtu.be/bltbJ2TUQWU?si=L07PNs15z8w26U6v) |
| Gemini or ChatGPT (for basic scripts I didn’t know) |
| Google, Google, and some more Google! |

</div>
