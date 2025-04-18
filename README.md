# SOC Core Skills with John Strand

## Course Summary

This 4-day course taught by John Strand provides a comprehensive foundation in core security operations center (SOC) skills. The course takes a hands-on, practical approach to teaching cybersecurity fundamentals through the lens of incident response, using the premise "you're compromised, now what?" rather than dry theoretical concepts. Throughout the course, students learn essential skills in networking, Linux and Windows systems, memory analysis, and security monitoring that form the building blocks for effective security operations.

## Key Takeaways

### Technical Foundations

- **Understanding the underlying technology is crucial**: Security tools abstract much of the technical complexity, but knowing how these systems actually work is essential for effective security analysis.
- **The TCP/IP model is more practical than OSI**: Focus on the 4-layer TCP/IP model (Network Access, Internet, Transport, Application) for real-world network analysis.
- **Think modularly with the "Lego approach"**: Build a toolkit of fundamental skills that can be combined in different ways to solve complex security problems.

### Investigation Methodology

- **Start with network connections**: When investigating suspicious activity, begin by examining network connections rather than processes to quickly narrow your focus.
- **Context is everything**: Individual security events rarely tell a complete story - correlation across multiple log sources provides the necessary context.
- **Defense in depth requires multiple detection methods**: Endpoint security, network monitoring, and log analysis all work together to provide comprehensive visibility.

### Practical Tools & Techniques

- **Command-line proficiency is essential**: Tools like tcpdump, lsof, grep, cut, and PowerShell commands are foundational for security analysis.
- **Memory analysis provides unique capabilities**: Memory forensics with tools like Volatility allows for investigation without alerting attackers.
- **Open-source tools can rival commercial solutions**: Free tools like Velociraptor, Wazuh, OWASP ZAP, and RITA provide powerful capabilities without high costs.

### Career Development

- **Focus on practical skills**: The industry needs analysts who understand fundamentals and can do hands-on investigation.
- **Research technology stacks**: When applying for jobs, study the company's technologies using resources like CIS Benchmarks to demonstrate initiative.
- **Detection tuning is a core skill**: There are no "false positives" - only detection tuning opportunities that analysts need to address.

## Day-by-Day Highlights

### Day 1: Networking Fundamentals

- TCP/IP concepts and packet structure
- Network communication and the 3-way handshake
- Using tcpdump and Wireshark for packet analysis
- Analyzing conversations between hosts

### Day 2: Linux & Windows Command Line

- Linux directory structure and command-line tools
- Using the /proc directory for process investigation
- Windows network connection analysis commands
- Process investigation with tasklist and wmic

### Day 3: Advanced Analysis Techniques

- Windows event log analysis with Deep Blue CLI
- Memory analysis with Volatility
- Network traffic analysis and beaconing detection
- RITA for identifying command and control traffic

### Day 4: Security Monitoring & Vulnerability Management

- User Entity Behavior Analytics (UEBA) concepts
- Endpoint Detection and Response (EDR) capabilities
- Efficient vulnerability management approaches
- Web application security testing with OWASP ZAP

## Resources

This repository contains detailed notes from each day of the course:

- [Day 1 - Networking Fundamentals](https://github.com/SOCScott/Antisyphon-SOC-Core-Skills/blob/main/Day%201%20-%20SOC%20Core%20Skills%20with%20John%20Strand%201d19e8f660dd804b93fbfa05df487c4f.md)
- [Day 2 - Linux & Windows Command Line](https://github.com/SOCScott/Antisyphon-SOC-Core-Skills/blob/main/Day%202%20-%20SOC%20Core%20Skills%20with%20John%20Strand%201d69e8f660dd80a1b031f11872535fd9.md)
- [Day 3 - Advanced Analysis Techniques](https://github.com/SOCScott/Antisyphon-SOC-Core-Skills/blob/main/Day%203%20-%20SOC%20Core%20Skills%20with%20John%20Strand%201d89e8f660dd80cdbe72cb350e04ac8c.md)
- [Day 4 - Security Monitoring & Vulnerability Management](https://github.com/SOCScott/Antisyphon-SOC-Core-Skills/blob/main/Day%204%20-%20SOC%20Core%20Skills%20with%20John%20Strand%201d99e8f660dd80869afaf0c1b83aba2a.md)

The course provides the core technical skills needed by SOC analysts while emphasizing the importance of continuous learning, research, and adaptability in the ever-changing cybersecurity landscape.
