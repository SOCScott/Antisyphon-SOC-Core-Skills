# SOC Core Skills with John Strand - Day 3

# SOC Core Skills with John Strand - Day 3 Notes

---

## Summary

Day 3 of SOC Core Skills with John Strand focuses on advanced analysis techniques for security operations. The session covers tools for automating security analysis, including Deep Blue CLI for Windows event log analysis, memory forensics with Volatility, and network traffic analysis with Rita/AC Hunter. Throughout the day, John emphasizes the importance of developing skills that go beyond basic tool operation, teaching techniques to identify sophisticated attacks like beaconing malware that uses legitimate cloud services. The labs provide hands-on experience with analyzing firewall logs, examining memory dumps, and detecting command and control traffic.

## Key Takeaways

1. Security analysis requires both automated tools and manual techniques - understanding how to use command-line tools like grep, cut, and statistical analysis helps analysts investigate logs from any device, not just those integrated with their SIEM.
2. Memory analysis is a powerful technique that allows investigators to examine compromised systems without alerting attackers, enabling process analysis, network connection examination, and command-line invocation recovery from memory dumps.
3. Beaconing detection is essential for identifying sophisticated malware that bypasses signature-based detection by using encryption and legitimate services like Microsoft and Amazon CDNs - look for patterns in intervals, data sizes, and connection duration.
4. When applying for security jobs, research the technology stack of the company and become familiar with security configurations by studying CIS benchmarks and hardening guides for those technologies.

## Detailed Notes

### Deep Blue CLI

- Created by Eric Conrad
- PowerShell-based security tool for Windows event log analysis
- Acts as a lightweight User Entity Behavior Analytics (UEBA) tool
- Helps identify suspicious patterns in Windows event logs
- Particularly useful for triage during incident response
- Can be used when an organization sends you event logs for analysis

### Deep Blue CLI Detection Capabilities:

- New user accounts added to administrator groups
- Password guessing attacks (multiple passwords against one account)
- Password spraying attacks (one password against multiple accounts)
- PowerShell/Command line obfuscation techniques:
    - Low percentage of alphanumeric characters
    - Excessive whitespace
    - Character-by-character encoding
    - Base64 encoding
    - Nested encoding techniques

### Advantages of Deep Blue CLI:

- Can analyze logs offline without needing direct system access
- Doesn't require a full SIEM deployment
- Helps identify patterns across multiple log entries
- Analyzes command line and PowerShell logging when enabled
- Has evolved into Deep White CLI (includes Sysmon event log analysis)

### Server Analysis and Technology Research

- When applying for security jobs, research the company's technology stack
- Use CIS Benchmarks and security guides to understand security-relevant settings
- Benefits:
    - Demonstrates initiative and learning ability
    - Shows ability to research independently
    - Provides practical knowledge about security configurations
    - Helps you understand where security-relevant settings are located
    - Improves interview performance

### Example PostgreSQL Security Settings:

- Looking at postmaster and backend runtime parameters
- Authentication roles and user permissions
- SSL mode configuration
- Network connections and ports

### Research approach:

1. Identify the technologies used by the target company
2. Find corresponding CIS Benchmarks or hardening guides
3. Set up the technology and apply recommended settings
4. Focus on security-relevant configurations:
    - Authentication
    - Permissions
    - Encryption
    - Logging
    - Network settings

### Firewall Log Analysis

### Lab Overview:

- Using Linux command-line tools to analyze Cisco ASA firewall logs
- Demonstrates techniques applicable to any log format
- Focuses on identifying beaconing behavior

### Key Commands and Techniques:

- `grep` - Find specific patterns or IP addresses
- `grep -v` - Exclude specific patterns
- `cut -d ' ' -f 1,3,4,5` - Extract specific fields/columns
- R-based statistical analysis

### Analysis Workflow:

1. Focus on a specific IP address of interest
2. Filter out noise (like edge router communications)
3. Look for patterns in connection behavior
4. Analyze data sizes and intervals
5. Perform statistical analysis to identify anomalies
6. Research IP addresses and domains (IPdb.info)

### Signs of Malicious Beaconing:

- Consistent intervals between connections
- Similar data sizes across connections
- Short connection durations
- Connections to legitimate-looking services (Microsoft/Amazon CDNs)
- Alternating connections between different destinations
- Low variance/standard deviation in connection patterns

### Memory Analysis with Volatility

### Advantages of Memory Analysis:

- Non-intrusive - doesn't alert attackers
- Works with systems you can't take offline
- Can extract deleted malware still resident in memory
- Works with cloud-based/virtualized assets (via snapshots)
- Reveals information even after system modification

### Volatility Framework:

- Open-source memory forensics tool
- Requires corresponding symbol tables for the OS version
- Analyzes memory dumps from Windows, Linux, Mac

### Key Volatility Commands:

- `malfind` - Identifies potential malware based on memory page permissions
- `netscan` - Shows network connections in memory
- `pslist` - Lists all processes
- `pstree` - Shows process hierarchy
- `dlllist` - Shows loaded DLLs for a process
- `cmdline` - Shows command line used to start a process

### Analysis Process:

1. Obtain memory dump (VM snapshot, hiberfil.sys, etc.)
2. Run `malfind` to identify suspicious processes
3. Use `netscan` to find established/suspicious connections
4. Examine process tree to understand process relationships
5. Analyze DLLs and command line parameters of suspicious processes
6. Look for lateral movement and privilege escalation

### Memory Analysis Observations:

- System process (PID 4) establishes SMB connections, not the application itself
- Closed or SYN_SENT connections may reveal previous activity
- Memory often contains remnants of connections after they're closed
- Process relationships reveal how malware executes
- Command line parameters show how processes were invoked

### Network Traffic Analysis

### Challenges with Modern Network Traffic:

- Encryption (SSL/TLS) prevents content inspection
- Legitimate services used for command and control
- High volume of normal traffic creates noise
- Varied network devices with different logging formats

### Net Flow:

- Statistical collection of network traffic data
- Cisco standard (NetFlow v9)
- Components:
    - Exporter: network device
    - Collector: storage system
    - Analyzer: system that analyzes data

### Zeek (formerly Bro):

- Industry standard for network monitoring
- Fast, consistent, with extensive community support
- Converts packet captures into structured logs
- Creates separate log types for different protocols
- No automatic detection or GUI - requires analysis

### RITA (Real Intelligence Threat Analytics):

- Free tool named after John's mother
- Uses Zeek logs for analysis
- Identifies non-human, beaconing traffic
- Checks against deny lists
- Analyzes DNS patterns
- Finds long connections

### Beaconing Detection:

- Looks for patterns in:
    - Connection intervals
    - Data sizes
    - Connection durations
- Uses statistical analysis to identify abnormal patterns
- Employs k-means clustering
- Can detect even when attackers try to randomize timing

### AC Hunter:

- Commercial version of RITA with GUI
- Web-based interface for analysis
- Shows beaconing scores and histograms
- Provides visual tools for investigation
- Available as Community Edition for home use

### Common Findings (Not Always Malicious):

- TeamViewer
- Remote Desktop Protocol (RDP)
- USB-to-Ethernet adapters
- Remote management tools
- Advertisement networks (block these to improve signal-to-noise ratio)

## Quiz Questions

1. **Question**: What technique can be used to analyze a potentially compromised system without alerting attackers who might be monitoring for security tools being run?
**Answer**: Memory analysis with tools like Volatility allows investigators to examine a memory dump of the system offline, revealing processes, network connections, and command line parameters without alerting attackers who are monitoring the live system.
2. **Question**: When analyzing firewall logs, what three key characteristics does RITA examine to identify potential beaconing malware?
**Answer**: RITA examines: 1) Connection intervals (timing between connections), 2) Data sizes (consistency in bytes transferred), and 3) Connection durations (how long connections remain open) to identify non-human traffic patterns that might indicate command and control activity.
3. **Question**: How do sophisticated attackers evade detection when using command and control servers, as demonstrated in the AC Hunter lab?
**Answer**: Sophisticated attackers evade detection by using legitimate cloud services (like Microsoft and Amazon CDNs) with good reputation scores, alternating connections between multiple destinations, employing encryption to hide content, and sometimes using techniques like DNS tunneling to bypass content inspection.
4. **Question**: What is one recommendation John Strand gives to improve your chances when applying for security jobs, especially regarding technology stacks you're not familiar with?
**Answer**: Research the company's technology stack before applying, download CIS benchmarks and security guides for those technologies, understand where security-relevant settings are located, and highlight this knowledge on your resume and during interviews to demonstrate your ability to learn and research independently.

## Notable Quotes

> "When you're looking at perfection in those [beacons], you use algorithms like k-means clustering... they're looking for clusters. Imagine each of the white dots represents an individual connection and we're analyzing those connections across multiple attributes."
> 

> "If you ever plan on going to court, one of the best things you can do is try to recreate your theory in a lab environment."
> 

> "The vast majority of SOC analysts rely exclusively based on what their tool tells them, and you can do that, you absolutely can do that...but you're the first in line to be laid off with AI."
> 

> "You may find people in your environment that are using TeamViewer. They're using TeamViewer to get to their home computer so they can surf porn, play video games and gamble without the filters in your environment. Now that's not malware, but is that absolutely something you want to investigate in your system? Absolutely."
> 

> "If I break that spaghetti, it's going to break into big pieces, little pieces, and it's going to shatter all over the place, but if I reassemble it, it's still going to be the same size as that spaghetti, which is a 24-hour period."
> 

> "These skills are table stakes. This is step level one. And unfortunately for the industry as it is right now, the people that are hiring aren't looking for junior level analysts that have a lot of heart and they're willing to learn and work hard. They're looking for people that understand these basic level skills."
> 

> "I had a theory that people were completely ignoring all traffic that went to Google and private email servers... We created a piece of malware called GCAT where all of the command and control went through well-formed email messages through Google... Almost every firewall on the face of the planet completely ignored any and all traffic to Google."
> 

> "If it's DNS, it's not DNS, couldn't be DNS, it's not possible, it's DNS, it was DNS."
>