# Week 1 — TCP, UDP, and Network Ports

## Objective
Understand TCP connections, UDP communication, network ports, and how to investigate network activity on a Windows computer.

## Tools Used
- Windows PowerShell
- `netstat`
- `Get-NetTCPConnection`
- `Get-Process`

## Part 1: TCP Connections

I used the following command to examine TCP connections:

`netstat -an -p tcp`

**Findings:**
- 36 established TCP connections
- 25 listening TCP entries
- At least one connection to remote port 443

I learned that an established connection indicates an active TCP connection, while a listening socket waits for incoming connections.

## Part 2: Investigating an Established Connection

I used PowerShell to identify the process responsible for a connection to port 443.

**Findings:**
- Process: Razer App Engine
- PID: 6936
- Remote port: 443

Port 443 is commonly associated with HTTPS. However, identifying a familiar program and port does not guarantee that a connection is safe.

## Part 3: Investigating Listening Ports

I examined listening TCP sockets and their local addresses.

**Findings:**
- 10 entries bound to `127.0.0.1`
- 12 entries bound to `0.0.0.0`
- TCP port 135 was listening on `0.0.0.0`

I learned that `127.0.0.1` is a loopback address, while `0.0.0.0` represents all IPv4 interfaces. Firewall rules still determine whether remote connections are permitted.

## Part 4: Investigating Port 135

I identified the process associated with TCP port 135.

**Findings:**
- Process: `svchost.exe`
- PID: 1192
- Port: 135/TCP

Port 135 is commonly associated with Microsoft's RPC Endpoint Mapper.

The observed process name is consistent with normal Windows activity, but additional verification would be needed to establish the service's legitimacy.

## Conclusion

During this lab, I learned how to:

1. Identify active TCP connections.
2. Distinguish established connections from listening sockets.
3. Associate network connections with process IDs.
4. Investigate processes using PowerShell.
5. Recognize common network ports.
6. Evaluate network activity without automatically assuming malicious behavior.

**Key takeaway:** A cybersecurity analyst should collect and evaluate evidence before determining whether network activity is suspicious.
