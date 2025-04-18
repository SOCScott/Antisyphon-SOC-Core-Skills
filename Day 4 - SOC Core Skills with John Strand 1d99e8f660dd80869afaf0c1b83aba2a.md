# SOC Core Skills with John Strand - Day 4

https://www.youtube.com/watch?v=YcG8gNSLTPQ

## Summary

Day 4 of SOC Core Skills with John Strand focuses on advanced security monitoring and detection technologies. The session covers User Entity Behavior Analytics (UEBA), Endpoint Detection and Response (EDR), vulnerability management, and web application security testing. Throughout the day, John emphasizes the importance of context in security alerts, demonstrates tools like Velociraptor for remote system investigation, and shows how to use open-source tools like OWASP ZAP for web vulnerability scanning. The class concludes with John discussing the importance of making security education accessible to all, highlighting Anti-Siphon's mission to break down barriers to entry in the cybersecurity field.

## Key Takeaways

1. User Entity Behavior Analytics (UEBA) works by correlating data from multiple log sources to identify suspicious patterns of behavior, such as password spraying attacks, rather than relying on isolated alerts from single systems.
2. When investigating potential security incidents, start by examining network connections to identify suspicious traffic patterns, then drill down to analyze the specific processes, command line parameters, and behaviors involved.
3. Open-source security tools like Velociraptor, Wazuh, and OWASP ZAP provide powerful capabilities for security monitoring, incident response, and vulnerability detection without the high costs of commercial solutions.
4. Vulnerability management should focus on grouping similar vulnerabilities across systems rather than addressing issues on an IP-by-IP basis, allowing for more efficient remediation through automation and configuration management.

## Detailed Notes

### User Entity Behavior Analytics (UEBA)

### What is UEBA?

- Examines patterns of user behavior across multiple systems
- Correlates data from various log sources to identify suspicious activity
- Provides context that isolated alerts lack
- Maps to various MITRE ATT&CK techniques

### How UEBA Works

- Looks at events across multiple systems and log sources:
    - Domain controllers
    - Workstations
    - Firewalls
    - Email servers
    - Network devices
- Uses stacking analysis and machine learning algorithms
- Sets thresholds for normal behavior and alerts on deviations
- Example: A single login might be normal, but logins to 200+ systems is suspicious

### Context in Security Events

- No single event log tells a complete story
- Security events require context from multiple sources
- John's analogy: "Walking through a forest" changes meaning when you add "along the beach"
- Events like "who am I" commands become more suspicious when combined with other commands
- Most security incidents require correlation across multiple events

### Detection Tuning Opportunities

- No such thing as "false positives" - only detection tuning opportunities
- Tuning is the job of security analysts
- Some organizations handle alerts differently:
    - Some create exceptions for legitimate processes
    - Others delete alerts entirely (not recommended)
- Risk-based alerting prioritizes:
    - Single repeating alerts (low priority)
    - Multiple different alerts (medium priority)
    - Network connection alerts (high priority)
    - Multiple systems affected (highest priority)

### Windows Event Log IDs for UEBA

- 4624/4625: Successful/failed login
- 4768/4769: Kerberos authentication
- 4776: NTLM authentication
- 4672: Special privileges assigned

### Deep Blue CLI Lab

- PowerShell-based tool for Windows event log analysis
- Can identify password spraying attacks
- Shows failed login attempts across multiple accounts
- Demonstrates how UEBA correlates multiple event logs

### Endpoint Detection and Response (EDR)

### Evolution of Endpoint Security

- Moved beyond traditional antivirus
- Incorporates behavioral analysis
- May include prevention capabilities
- Some vendors expanding to XDR (Extended Detection and Response)

### MITRE ATT&CK Evaluations

- Tests EDR products against known attack techniques
- Limitation: vendors can tune specifically for the evaluation
- Not a true competition between products
- Does not accurately represent real-world bypass techniques

### Benefits of EDR Over Traditional AV

- Uses machine learning instead of just signatures
- Hooks into operating system for better visibility
- Can identify previously unknown threats
- Typically uses a combination of:
    - Deny lists (known bad)
    - Allow lists (known good)
    - Gray lists (analyzed in sandbox)

### Open-Source EDR Options

- Wazuh:
    - Free, open-source security monitoring
    - Includes vulnerability management
    - Good dashboards and visualization
    - Can monitor Docker containers
- Velociraptor:
    - Small, efficient binary
    - Great for incident response
    - Can query multiple systems simultaneously
    - Remote command execution and file access
    - Hunting capabilities across systems

### Velociraptor Lab

- Installing and configuring Velociraptor server and client
- Creating users and setting up the environment
- Running commands on connected systems
- Creating hunts to collect information from endpoints
- Analyzing process trees and network connections

### Other Free/Open-Source Options

- Lima Charlie (free tier available)
- Elastic Security (free open-source option)
- Huntress (neighborhood watch program)
- Komodo Open EDR

### Vulnerability Management

### Current State of Vulnerability Management

- Little innovation in the past decade
- Organizations focus too much on high/critical vulnerabilities
- Often ignore medium/low/informational issues
- Creates blind spots for attackers to exploit

### Example of Dangerous "Low" Vulnerabilities

- Telnet servers with no authentication
- Inappropriate focus on CVSS scores rather than actual risk
- Vulnerabilities labeled as "low" can still be highly exploitable

### Effective Vulnerability Management Approach

- Group vulnerabilities by type rather than by IP address
- Example: 1,000 IPs with 25 vulnerabilities each
    - Traditional approach: 25,000 issues to fix individually
    - Better approach: Fix similar vulnerabilities across systems
- Use automation tools (Ansible, Puppet, Chef, GPO) to remediate at scale
- Apply the 80/20 (or 90/10) rule to prioritize effectively

### Vulnerability Management Limitations

- Only covers a small portion of MITRE ATT&CK matrix
- Need to supplement with threat emulation
- Should be part of a continuous security program

### Web Application Security

### Challenges with Web App Security

- Custom web applications have unique vulnerabilities
- Traditional vulnerability scanners don't effectively detect web app issues
- Security often "bolted on" at the end of development
- Training and tools can be expensive

### Automated vs. Manual Testing

- Automated tools can find 80-90% of common vulnerabilities:
    - Cross-site scripting (XSS)
    - SQL injection
    - Command injection
    - Misconfigurations
- Manual testing needed for:
    - Business logic errors
    - Permission issues
    - Stored XSS
    - Cross-site request forgery (CSRF)

### Web Application Testing Tools

- Burp Suite Pro (commercial)
- OWASP ZAP (free, open-source)
- Nikto (free, open-source)
- All provide proxy functionality and automated scanning

### OWASP ZAP Lab

- Starting a vulnerable web application (DVWA)
- Configuring ZAP as a proxy
- Running automated scans against the application
- Identifying vulnerabilities like SQL injection and XSS
- Examining details about discovered vulnerabilities

## Quiz Questions

1. **Question**: How does User Entity Behavior Analytics (UEBA) differ from traditional security monitoring approaches?
    - **Answer**: UEBA correlates data from multiple log sources (domain controllers, workstations, firewalls, email servers, etc.) to identify suspicious patterns of behavior, rather than generating isolated alerts from individual systems. It uses techniques like stacking analysis and machine learning to establish baselines of normal behavior and detect deviations, providing context that single-point monitoring cannot.
2. **Question**: According to John Strand, what approach should organizations take when handling "false positives" in their security tools?
    - **Answer**: John argues that "false positives" don't exist - they should be viewed as "detection tuning opportunities." Instead of deleting alerts entirely, organizations should refine their detection rules to accommodate legitimate business processes while still maintaining visibility into potential threats. This puts responsibility on analysts to improve detection rather than blaming the alerts themselves.
3. **Question**: What makes Velociraptor valuable as an incident response tool, and how does it differ from full EDR solutions?
    - **Answer**: Velociraptor is valuable for its ability to remotely investigate systems, run commands across multiple endpoints simultaneously, access file systems, and collect forensic data without alerting attackers. It differs from full EDR solutions in that it lacks prevention capabilities and automatic detection, focusing instead on investigation and response capabilities with a small, efficient binary footprint.
4. **Question**: What fundamental shift in vulnerability management strategy does John Strand recommend, and why is it more effective?
    - **Answer**: John recommends grouping vulnerabilities by type rather than addressing them IP-by-IP. Instead of fixing each vulnerability individually across systems, organizations should use automation tools like Ansible, Puppet, or Group Policy to remediate similar vulnerabilities across all affected systems simultaneously. This approach can address hundreds or thousands of instances of the same vulnerability through a single configuration change, dramatically increasing efficiency.

## Notable Quotes

> "There's no event log that is a straight up 'you've been hacked' event log. It requires context of a number of event logs to be able to tell that story, to be able to explain what's going on."
> 

> "False positives are not a thing, they just aren't. If you're looking at PowerShell execution, an organization may have a legitimate service that runs PowerShell... but some organizations will handle that alert differently."
> 

> "Plans are useless. Planning is indispensable."
> 

> "If you're trying to figure out how to triage and work in your environment... a single repeating alert, not all that interested. Multiple different alerts, now all of a sudden the SOC has got to interact with that. If you have network connections, stop everything, we're going to start isolating systems."
> 

> "There are a lot of vendors out there that if you want to try their tool, you literally have to pay like in escrow something like $100,000... and that's just absolutely horrible. To just evaluate a product. And usually that shows that people don't have a lot of faith in their tools."
>
