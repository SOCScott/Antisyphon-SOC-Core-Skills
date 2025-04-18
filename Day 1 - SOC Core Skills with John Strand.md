# SOC Core Skills w/ John Strand - Day 1

https://www.youtube.com/watch?v=IHlcnAUMlzE

## Summary

This set of notes covers Day 1 of the SOC Core Skills course with John Strand, which focuses on fundamental skills necessary for security professionals. The course takes a practical approach by examining security concepts through the lens of incident response and compromise scenarios rather than dry technical explanations. John covers TCP/IP networking fundamentals, packet analysis with tcpdump and Wireshark, and emphasizes the importance of mastering core skills rather than relying solely on security tools. The course is designed to build a foundation for security analysis by teaching participants how to understand the underlying technologies they'll encounter in security roles.

## Key Takeaways

1. Core technical fundamentals (Windows, Linux, TCP/IP) are essential for security professionals, as all security tools ultimately rely on these foundations.
2. The TCP/IP model (Network Access, Internet, Transport, Application) is more practically useful than the OSI model for understanding how networks actually function.
3. Effective incident response requires building a toolkit of fundamental skills (like "Legos") that can be assembled to solve complex security problems.
4. Packet analysis tools like tcpdump and Wireshark are complementary - tcpdump excels at high-speed data capture, while Wireshark is superior for in-depth packet analysis and visualization.

## SOC Core Skills - Day 1 Study Notes

### Course Overview and Philosophy

- The course focuses on fundamental skills considered critical for security professionals
- Covers Windows, Linux, and TCP/IP networking
- Designed as a foundation for the Intro To Security class and Cyber Deception
- Uses a "you're compromised, now what?" approach to teach concepts
- Part of Anti-Siphon's "pay what you can" training model to make security education accessible

### The "Lego" Approach to Incident Response

- Complex problems don't require overly complex solutions
- Detailed flowcharts and extensive procedures are often impractical during real incidents
- Instead, build with "Legos" of functionality - modular skills that can be combined as needed
- References "Backdoors and Breaches" card game which demonstrates this modular approach
- Skills like network threat hunting, memory analysis, and endpoint analysis are the building blocks

### TCP/IP vs OSI Model

- John strongly advocates for the TCP/IP model over the OSI model
- The OSI model was created 35+ years ago before modern networking existed
- TCP/IP better reflects how networks actually function today
- TCP/IP has 4 layers: Network Access (physical/Ethernet), Internet (IP), Transport (TCP/UDP), Application
- OSI's separation into 7 layers (especially session, presentation, application) was the result of consensus-building rather than technical reality

### IP Fundamentals

- IP addresses are 32-bit numbers (IPv4) that uniquely identify systems on the internet
- IP headers contain crucial information:
    - Version (IPv4, IPv6)
    - Length
    - Type of service
    - Identification, flags, and fragmentation offset (for packet fragmentation)
    - Time to live (TTL)
    - Protocol
    - Checksum
    - Source and destination addresses

### TCP/UDP Fundamentals

- Every computer has 65,536 ports for TCP and 65,536 ports for UDP (16-bit values)
- Ports are like "rooms" in a hotel where different services reside
- Common ports: 80 (HTTP), 443 (HTTPS), 22 (SSH), 23 (Telnet), 3389 (RDP)
- TCP vs UDP:
    - TCP: Connection-oriented, reliable (sequence/acknowledgment numbers)
    - UDP: Connectionless, "fire and forget," good for streaming
- TCP flags (SYN, ACK, FIN, RST, PSH, URG) control communication flow
- TCP 3-way handshake: SYN → SYN-ACK → ACK

### Packet Analysis Tools

- tcpdump:
    - Command-line tool
    - Great for high-speed data capture
    - Good for scripting and automation
    - Can filter traffic, show ASCII/hex output
    - Used for initial triage and data collection
- Wireshark:
    - GUI-based tool
    - Excellent for in-depth packet analysis
    - Color-coding for different protocols
    - Can follow TCP streams to reconstruct conversations
    - Provides statistical analysis (conversations, protocols)
    - Better for detailed examination of specific traffic

### Practical Analysis Techniques

- Looking at conversations between hosts (who's talking to whom and how much)
- Following TCP streams to view full communication
- Analyzing HTTP requests to identify suspicious domains
- Using filters to focus on specific traffic (HTTP, ICMP, etc.)
- Examining packet headers for unusual patterns
- Identifying beaconing behavior from malware

### Industry Insights and Career Advice

- Entry-level security job market is currently challenging
- Universities and certifications often fail to teach practical skills
- Anti-Siphon's approach focuses on real-world, applicable skills
- Learning these core fundamentals makes you more valuable

## Quiz Questions

1. **Question**: What are the four layers of the TCP/IP model that John Strand recommends using instead of the OSI model?
    - **Answer**: Network Access (physical/Ethernet), Internet (IP), Transport (TCP/UDP), and Application.
2. **Question**: In the TCP 3-way handshake, what happens when the acknowledgment number is one more than the sequence number in the response packet?
    - **Answer**: This is normal behavior - the acknowledgment number increments the received sequence number by one to confirm receipt of the SYN packet.
3. **Question**: Why does John Strand describe his approach to incident response as using "Legos" of functionality?
    - **Answer**: Because complex security problems can be solved by assembling modular skills (like Lego bricks) rather than following rigid, complex procedures. These fundamental skills can be combined in different ways to address various security scenarios.
4. **Question**: What are the primary differences between tcpdump and Wireshark that determine when you would use each tool?
    - **Answer**: tcpdump is a command-line tool best for high-speed data capture, scripting, and initial triage, while Wireshark is a GUI tool that excels at in-depth packet analysis, visualization of traffic, and detailed examination of specific communications.

## Notable Quotes

> "The reality is we have to understand how the underlying components work for the technologies that are abstracted for us."
> 

> "Plans are useless. Planning is indispensable."
> 

> "When you're dealing with an incident and we're really focusing on the incident lens, right, is don't panic."
> 

> "If you know how to use these basic core fundamental Lego bricks, you can deal with any level of complexity in the form of an attack by utilizing these and stacking them together correctly."
>
