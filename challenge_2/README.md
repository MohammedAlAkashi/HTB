## target HOST: 10.129.203.65
## target OS: Windows

### nMap scan output:

```
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-05-01 03:27 EDT
Nmap scan report for 10.129.203.65
Host is up (0.032s latency).
Not shown: 995 closed tcp ports (reset)
PORT     STATE SERVICE       VERSION
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds?
3389/tcp open  ms-wbt-server Microsoft Terminal Services
|_ssl-date: 2024-05-01T07:28:22+00:00; +1s from scanner time.
| ssl-cert: Subject: commonName=WIN-51BJ97BCIPV
| Not valid before: 2024-04-30T07:06:57
|_Not valid after:  2024-10-30T07:06:57
| rdp-ntlm-info: 
|   Target_Name: WIN-51BJ97BCIPV
|   NetBIOS_Domain_Name: WIN-51BJ97BCIPV
|   NetBIOS_Computer_Name: WIN-51BJ97BCIPV
|   DNS_Domain_Name: WIN-51BJ97BCIPV
|   DNS_Computer_Name: WIN-51BJ97BCIPV
|   Product_Version: 10.0.17763
|_  System_Time: 2024-05-01T07:28:13+00:00
5000/tcp open  http          Microsoft IIS httpd 10.0
|_http-title: FortiLogger | Log and Report System
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.94SVN%E=4%D=5/1%OT=135%CT=1%CU=41143%PV=Y%DS=2%DC=T%G=Y%TM=6631
OS:EF15%P=x86_64-pc-linux-gnu)SEQ(SP=107%GCD=1%ISR=10C%TI=I%CI=I%II=I%SS=S%
OS:TS=U)OPS(O1=M53CNW8NNS%O2=M53CNW8NNS%O3=M53CNW8%O4=M53CNW8NNS%O5=M53CNW8
OS:NNS%O6=M53CNNS)WIN(W1=FFFF%W2=FFFF%W3=FFFF%W4=FFFF%W5=FFFF%W6=FF70)ECN(R
OS:=Y%DF=Y%T=80%W=FFFF%O=M53CNW8NNS%CC=Y%Q=)T1(R=Y%DF=Y%T=80%S=O%A=S+%F=AS%
OS:RD=0%Q=)T2(R=Y%DF=Y%T=80%W=0%S=Z%A=S%F=AR%O=%RD=0%Q=)T3(R=Y%DF=Y%T=80%W=
OS:0%S=Z%A=O%F=AR%O=%RD=0%Q=)T4(R=Y%DF=Y%T=80%W=0%S=A%A=O%F=R%O=%RD=0%Q=)T5
OS:(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=80%W=0%S=A%A=O
OS:%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=80%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=
OS:N%T=80%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=80%
OS:CD=Z)

Network Distance: 2 hops
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time: 
|   date: 2024-05-01T07:28:17
|_  start_date: N/A
|_clock-skew: mean: 1s, deviation: 0s, median: 1s
| smb2-security-mode: 
|   3:1:1: 
|_    Message signing enabled but not required

TRACEROUTE (using port 3306/tcp)
HOP RTT      ADDRESS
1   34.71 ms 10.10.14.1
2   34.77 ms 10.129.203.65

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 32.29 seconds
```
Target host had a outdated and vulnerable version of **Fortilogger**
Microsoft IIS httpd 10.0 alone was outdated and vulnerable, however, nMaps insight allowed me to find the proper exploit to use on the host machine

# Exploitation
## Exploits used:
FortiLogger Arbitrary File Upload Exploit  
CVE-2021-3378,
[github](https://erberkan.github.io/2021/cve-2021-3378/)

## Post Exploitation
the challenge required me to find the NTLM hash of a specific user
thankfully the host machine was authenticated as administerator
```
lsa_dump_secrets
```
dumped all the hashes (including NTLM hashes) which allowed me to find
the specific one i needed, which in return concluded the challenge.
