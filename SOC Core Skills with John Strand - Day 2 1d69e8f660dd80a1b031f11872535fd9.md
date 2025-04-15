# SOC Core Skills with John Strand - Day 2

https://www.youtube.com/watch?v=QCzsliXu-z0

## Summary

Day 2 of SOC Core Skills with John Strand focuses on Linux and Windows system fundamentals through the lens of incident response. Rather than teaching these operating systems in a dry, theoretical manner, John demonstrates how to investigate potentially compromised systems using practical command-line tools and techniques. The class covers Linux directory structures, essential commands, and processes, then transitions to Windows commands for network connection analysis and process investigation. Throughout the session, hands-on labs reinforce these concepts, including creating and hunting for backdoors on Linux and investigating malware on Windows systems.

## Key Takeaways

1. When investigating suspicious activity, start with network connections rather than processes - this narrows your focus and helps identify potential malware more efficiently.
2. In Linux, everything is represented as a file (including devices, directories, and processes), and understanding how to navigate the file system is crucial for forensic analysis.
3. The `/proc` directory in Linux contains runtime information about processes, allowing analysts to extract memory-resident malware even after the original executable has been deleted.
4. Windows command-line tools like `netstat -naob` and `tasklist /svc` provide essential visibility into network connections, process information, and loaded DLLs - critical for identifying malicious activity.

## **SOC Core Skills - Day 2 Study Notes**

### Linux Fundamentals

### Directory Structure Overview

- `/` - Root directory, top level of the file system hierarchy
- `/bin` - Binary files and executables
- `/boot` - Boot files, kernel images, and boot manager configurations
- `/dev` - Device files (everything in Linux is represented as a file)
- `/etc` - System configuration files
- `/home` - User home directories
- `/lib` - Libraries (shared code used by applications)
- `/media` - Mount points for removable media
- `/mnt` - Mount points for temporary file systems
- `/opt` - Optional software packages
- `/proc` - Process information (virtual file system)
- `/root` - Home directory for the root user
- `/run` - Runtime data
- `/sbin` - System binaries (admin commands)
- `/srv` - Service data
- `/sys` - System files
- `/tmp` - Temporary files
- `/usr` - User programs
- `/var` - Variable data (logs, mail, etc.)

### Essential Linux Commands

- `ls` - List files and directories
- `ls -a` - Show hidden files (files starting with `.`)
- `ls -lrt` - Long listing with details, sorted by time
- `cd` - Change directory
- `pwd` - Print working directory
- `mkdir` - Make directory
- `locate` - Find files by name (uses a database)
- `update-db` - Update the locate database
- `which` - Show which executable will run for a command
- `vi`/`vim`/`nano` - Text editors
- `cat` - Display file contents
- `ps` - Display process information
- `ps aux` - Show all processes with details
- `top` - Interactive process viewer
- `ifconfig`/`ip a` - Show network interface information
- `ping` - Test network connectivity
- `nmap` - Network scanner
- `netstat` - Show network connections
- `lsof` - List open files
- `lsof -i` - List open internet connections
- `sudo su -` - Become root with environment variables

### Hidden Files in Linux

- Files starting with a `.` are hidden by default
- User configuration files are typically stored as hidden files in home directories
- View hidden files with `ls -a`

### Processes in Linux

- Each process has a unique Process ID (PID)
- Processes can be viewed with `ps`, `top`, and other tools
- `/proc` directory contains information about running processes
    - `/proc/[PID]` - Directory for each process
    - `/proc/[PID]/exe` - Link to the executable in memory
    - `/proc/[PID]/cmdline` - Command line arguments

### Network Commands

- `ifconfig` - Display network interfaces (traditional)
- `ip a` - Display network interfaces (newer command)
- `ping` - Test network connectivity ("packet internet groper")
- `nmap` - Network scanner for open ports
- `netstat` - Display network connections
- `lsof -i` - List open network files/connections

### Linux Backdoor Lab

- Creating a FIFO (First In, First Out) "backpipe" for covert communication
    - `mknod backpipe p` creates a special file for inter-process communication
    - Backdoor command: `bin/bash < backpipe | nc -l -p 2222 > backpipe`
    - This creates a backdoor listening on port 2222
- Finding malware on Linux:
    1. Use `lsof -i -P` to identify suspicious network connections
    2. Note the process ID (PID) of suspicious processes
    3. Use `lsof -p [PID]` to see all files opened by the process
    4. Check `/proc/[PID]/exe` to examine the executable in memory
    5. Use `strings` against the executable to see readable text
    6. Even if malware deletes itself, it remains in memory and can be extracted
        - `lsof +L1` shows deleted files still open by processes
        - Copy `proc/[PID]/exe` to extract memory-resident malware

### Windows Command Line

### Network Connection Analysis

- `net view` - Display network shares
- `net use` - Show outbound SMB connections (what this system is connecting to)
- `net session` - Show inbound SMB connections (who's connecting to this system)
- `netstat` - Show network connections
    - `netstat -naob` - Show all connections with process IDs and executable names
        - n = Don't resolve names
        - a = Show all connections
        - o = Show owner process ID
        - b = Show executable
    - `netstat -f` - Show fully qualified domain names

### Process Analysis

- `tasklist` - Show running processes
    - `tasklist /svc` - Show services running in each svchost.exe
    - `tasklist /m` - Show DLLs loaded by each process
    - `tasklist /m [DLL]` - Show processes using a specific DLL
    - `tasklist /fi "PID eq [PID]"` - Filter by process ID
- `wmic` (Windows Management Instrumentation Command)
    - `wmic process list full` - Detailed process information
    - `wmic process where processid=[PID] get commandline` - Show command line
    - `wmic process get name,processid,parentprocessid` - Show process hierarchy

### Windows Command Line Lab

1. Set administrator password and disable Windows Defender
2. Use Metasploit from Linux to execute malware on Windows
    - `use exploit/windows/smb/psexec`
    - Set payload, remote host, username, and password
    - Run the exploit to create a backdoor connection
3. Investigate the malware:
    - Use `netstat -naob` to identify suspicious connections
    - Look for PowerShell processes with established connections
    - Use `tasklist /fi "PID eq [PID]"` to examine the process
    - Use `wmic process where processid=[PID] get commandline` to see the command
    - Examine loaded DLLs to identify malicious behavior

## Quiz Questions

1. **Question**: In Linux, why is the `/proc` directory important for malware investigation?
    - **Answer**: The `/proc` directory contains runtime information about processes, including a link to the executable in memory (`/proc/[PID]/exe`). This allows investigators to examine and extract malware even if the original file has been deleted from the disk, as it remains in memory until the process terminates.
2. **Question**: When investigating a potentially compromised Windows system, why is it recommended to start with network connection analysis rather than process analysis?
    - **Answer**: Starting with network connections narrows the focus to processes that are actively communicating, making it easier to identify potential malware. Commands like `netstat -naob` show established connections with their associated process IDs and executable names, providing immediate leads for investigation.
3. **Question**: What Linux command would you use to find all deleted files that are still being used by processes?
    - **Answer**: The command `lsof +L1` shows all files with a link count less than 1, which indicates files that have been deleted from the file system but are still open by processes. This is useful for finding malware that deletes itself after execution but remains running in memory.
4. **Question**: How can you identify which Windows services are running within multiple instances of svchost.exe?
    - **Answer**: The command `tasklist /svc` will show which specific Windows services are running within each instance of svchost.exe. This transforms the generic svchost.exe process information into actionable data that reveals the actual services being executed.

## Notable Quotes

> "Everything in Linux and Unix is a file. Directories are a file with directory attributes, files are files, some files are executable, some files are not, some files are first-in first-out device files, some devices are also represented by files."
> 

> "These skills are fundamental. We're doing this because we feel like most people don't have these skills. We're doing this and we're making it accessible."
> 

> "The ultimate goal of what we're trying to do here is we are trying to transfer data between multiple processes, but we're transferring that data across these processes utilizing backpipe as that hidden back door."
> 

> "If you start at the network connections, that really limits the number of processes that you have to look at."
> 

> "Windows Defender is like 'Oh look there's malware!' A lot of people will be like 'Well it got it.' Not necessarily. A huge percentage of our work, the customer got an AV alert, but it didn't fire fast enough and the malware was able to start spreading before they were able to stop it."
>
