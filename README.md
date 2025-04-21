# Detection Lab (SIEM)

![Screenshot 2025-04-19 160523](https://github.com/user-attachments/assets/6bc14c54-926e-4da0-9b09-a1e27919f8c1)
*Ref 1: Traffic, logs, and alerts visualized through Security Onion’s dynamic dashboard.*

<blockquote style="border-left: 3px solid #dfe2e5; color: #6a737d; padding: 0 1em; margin: 24px 0;">
    <strong>Note:</strong> This was Security Onion's captured traffic after the initial setup.
  </blockquote>
</div>

## Objective

To build a controlled Security Information and Event Management (SIEM) lab environment for detecting, analyzing, and responding to simulated cyber threats. The lab integrates log sources (Windows/Linux systems, network devices, and applications) with a SIEM to enable real-time monitoring, correlation, and alerting.

## Skills Learned

### Core Skills Developed
- Deployed Security Onion with Elastic Stack (Elasticsearch, Kibana) for SIEM/NSM
- Configured Suricata (IDS/IPS) and Zeek for network traffic analysis
- Simulated attacks (Nmap scans, brute force, web attacks) to test detection
- Analyzed logs in Kibana and correlated security events
- Performed incident response triage and documentation

### Technical Proficiencies
- Security Onion administration (`sosetup`, `so-status`)
- Suricata rule creation and tuning
- Zeek network protocol analysis
- Kibana dashboard creation and log investigation
- Network forensics and IOC identification

## Tools Mastered
- Security Onion (SIEM/NSM platform)
- Suricata (signature-based detection)
- Zeek (network metadata analysis)
- Elastic Stack (log storage/visualization)

<blockquote style="border-left: 3px solid #dfe2e5; color: #6a737d; padding: 0 1em; margin: 24px 0;">
    <strong>Note:</strong> Security Onion was deployed with dynamic IP range-based monitoring rather than static host assignments, expanding visibility to all connected devices.
  </blockquote>
</div>

<div style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif; max-width: 800px; margin: 0 auto; color: #24292e; line-height: 1.5;">
  <h2 style="border-bottom: 1px solid #eaecef; padding-bottom: 0.3em;">Steps</h2>

  <div style="margin-bottom: 24px;">
    <h3 style="margin-bottom: 16px; margin-top: 24px;">Requirements</h3>
    <ul style="padding-left: 20px;">
      <li>16GB RAM (8GB minimum)</li>
      <li>4 CPU cores</li>
      <li>100GB disk space</li>
      <li>Virtualization (VMware/VirtualBox/Proxmox)</li>
    </ul>
  </div>

  <div style="margin-bottom: 24px;">
    <h3 style="margin-bottom: 16px; margin-top: 24px;">Setup Steps</h3>
    <ol style="padding-left: 20px;">
      <li><strong>Install Security Onion ISO on VM</strong></li>
      <li><strong>Run initial configuration:</strong>
        <div style="background: #f6f8fa; padding: 12px; border-radius: 6px; border-left: 3px solid #0366d6; margin: 8px 0; font-family: monospace; font-size: 14px;">
          sudo sosetup<br>
          - Choose Evaluation Mode<br>
          - Enable Zeek + Suricata + Elastic Stack<br>
          - Set admin password
        </div>
      </li>
    </ol>
  </div>

  <div style="margin-bottom: 24px;">
    <h3 style="margin-bottom: 16px; margin-top: 24px;">Access Interfaces</h3>
    <div style="background: #f6f8fa; padding: 12px; border-radius: 6px; border-left: 3px solid #0366d6; font-family: monospace; font-size: 14px;">
      - Web UI: https://[your-IP]<br>
      - Kibana: https://[your-IP]/kibana<br>
      - Hunt: https://[your-IP]/hunt
    </div>
  </div>

  <div style="margin-bottom: 24px;">
    <h3 style="margin-bottom: 16px; margin-top: 24px;">Attack Commands (Linux)</h3>
    <div style="background: #f6f8fa; padding: 12px; border-radius: 6px; border-left: 3px solid #0366d6; font-family: monospace; font-size: 14px;">
      nmap -sV [target_IP]<br>
      curl -A "malicious" http://[target_IP]
    </div>
  </div>
  
![Screenshot 2025-04-19 162643](https://github.com/user-attachments/assets/20b0d50d-2f4f-48e7-9e3d-04bdc16c3694)
*Ref 2: List of alerts and potential threats.*

  <div style="margin-bottom: 24px;">
    <h3 style="margin-bottom: 16px; margin-top: 24px;">Attack Commands (Windows)</h3>
    <div style="background: #f6f8fa; padding: 12px; border-radius: 6px; border-left: 3px solid #0366d6; font-family: monospace; font-size: 14px;">
      crowbar -b rdp -s [target_IP] -u admin -w wordlist.txt<br>
      powershell -c "Invoke-WebRequest http://[target_IP]"
    </div>
    <blockquote style="border-left: 3px solid #dfe2e5; color: #6a737d; padding: 0 1em; margin: 16px 0;">
      <strong>Brute Force Testing:</strong> Conducted RDP brute-force attempts against admin accounts using Crowbar to test detection capabilities.
    </blockquote>
  </div>
  
![Screenshot 2025-04-19 164538](https://github.com/user-attachments/assets/c2fe9773-ce43-4128-8077-884aee140a41)
*Ref 3: Alerts showing 4 failed login attempts using ssh.*
  <div style="margin-bottom: 24px;">
    <h3 style="margin-bottom: 16px; margin-top: 24px;">Kibana Searches</h3>
    <div style="background: #f6f8fa; padding: 12px; border-radius: 6px; border-left: 3px solid #0366d6; font-family: monospace; font-size: 14px;">
      event.module: "suricata" and alert.signature: "HTTP"<br>
      event.dataset: "zeek.http" and http.user_agent: "malicious"
    </div>
  </div>

  <blockquote style="border-left: 3px solid #dfe2e5; color: #6a737d; padding: 0 1em; margin: 24px 0;">
    <strong>Note:</strong> This implementation focuses on core steps while maintaining security testing best practices. Brute-force testing was conducted in a controlled lab environment.
  </blockquote>
</div>


![Screenshot 2025-04-19 163331](https://github.com/user-attachments/assets/52e080f3-43c7-4b2d-8d8f-50d9f74f88cd)

*Ref 4: Alternate view of login failures.*


 <blockquote style="border-left: 3px solid #dfe2e5; color: #6a737d; padding: 0 1em; margin: 24px 0;">
    <strong>Note:</strong> With Security Onion, alerts can be viewed through different tools, offering a degree of customization in workflow.
  </blockquote>
</div>
