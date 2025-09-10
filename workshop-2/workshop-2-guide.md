
# Workshop 2 Guide (Kali Linux Walkthrough & Networking)

*Author: Tay Jovan*  
*Last updated: 2025/09/10*

## 0. Outline

- [1. Kali Linux Basics](#1-kali-linux-basics)
- [2. Basic Commands](#2-basic-commands)
- [3. Kali Tweaks](#3-kali-tweaks)
- [4. Cyber Kill Chain](#4-cyber-kill-chain)
- [5. Networking Tools](#5-networking-tools)
  - [5.1. Nmap](#51-nmap)
  - [5.2. Analysing Network Traffic](#52-analysing-network-traffic)
    - [5.2.1. Tcpdump](#521-tcpdump)
    - [5.2.2. Wireshark](#522-wireshark)
- [6. References](#6-references)

## 1. Kali Linux Basics

Login in to Kali Linux with the default credentials `kali : kali`:


![](workshop-2-images/Pasted%20image%2020250909183341.png)

To open your terminal, either click on the terminal icon or use the keyboard shortcut `ctrl + alt + T`:

![](workshop-2-images/terminal.png)

![](workshop-2-images/{3A4BD218-49CA-43CF-9432-9A6594ED4E3C}.png)

To access your terminal settings, go to `File > Preferences`:

![](workshop-2-images/{4BA8A17C-B128-4B91-824D-11296E148FAD}.png)

![](workshop-2-images/settings.png)

To view keyboard shortcuts, click on `Shortcuts`:

![](workshop-2-images/shortcuts.png)

Common shortcuts:
- New tab: `Ctrl + Shift + T`
- New window: `Ctrl + Shift + N`
- Move between tabs: `Ctrl + Tab` or `Ctrl + PgUp/PgDown`
- Close tab: `Ctrl + Shift + W`
- Split left/right: `Ctrl + Shift + R`
- Split up/down: `Ctrl + Shift + D`
- Move between panes: `alt + arrow keys`
- Close pane: `Ctrl + Shift + E`

## 2. Basic Commands

To check which directory you are currently in:

```
pwd
```

To list directory contents:

```
ls
```

To list all directory contents (including hidden files) in long listing format:

```
ls -la
```

To read a file contents:

```
cat <file>
```

To change directories:

```
cd
```

If we don't specify a directory, by default the system will return us to our home directory (`/home/$USER`).

![](workshop-2-images/directory-diagram.png)

To change to the parent directory:

```
cd ..
```

To change back to the your home directory:

```
cd
```

To check the manual of a command:

```
man <command>
```

To see your command history:

```
history
```

To check your user ID:

```
id
```

To run a command as root temporarily:

```
sudo <command>
```

To update and upgrade your system:

```
sudo apt update && sudo apt upgrade -y
```
## 3. Kali Tweaks

Tweaks for Kali Linux, including:
- Shell configuration
- APT mirrors configuration
- Kali Linux metapackages installation and removal
- Hardening of the system
- Additional configuration for virtualized environments
- Kernel settings

To run kali tweaks:

```
kali-tweaks
```

![](workshop-2-images/{80FEC4B9-3C64-4B23-9262-FCCA1ECF1DC6}.png)

## 4. Cyber Kill Chain

The seven steps of the Cyber Kill Chain is as follows ([Lockheed Martin](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html)):
- **Reconnaissance**: This is the stage we are covering today. This includes both active and passive reconnaissance, where you are gathering information about the target.
- **Weaponisation**: creates a malicious payload (e.g., malware, exploit code, phishing email).
- **Delivery**: The attacker transmits the weapon to the target.
- **Exploitation**: The malicious code is triggered, exploiting a vulnerability to gain access.
- **Installation**: Installs backdoors, Trojans, or other persistence mechanisms on the compromised system.
- **Command & Control**: The compromised system establishes a communication channel with the attacker’s server to receive instructions.
- **Action on Objectives**: achieves their goals, such as data theft, ransomware deployment, system sabotage, or espionage.

![](workshop-2-images/Pasted%20image%2020250910123908.png
)
## 5. Networking Tools

### 5.1. Nmap


> Nmap is used to discover hosts and services on a computer network by sending packets and analyzing the responses. ([Wikipedia](https://en.wikipedia.org/wiki/Nmap))


```
nmap scanme.nmap.org
```

```
root@kali:~# nmap scanme.nmap.org
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-10 12:24 +08
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.22s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 994 closed tcp ports (reset)
PORT      STATE    SERVICE
21/tcp    open     ftp
22/tcp    open     ssh
25/tcp    filtered smtp
80/tcp    open     http
9929/tcp  open     nping-echo
31337/tcp open     Elite

Nmap done: 1 IP address (1 host up) scanned in 8.52 seconds
```

There are a total of 6 different states for a scanned port we can obtain, with the 3 main ones being:
- `open`: connection to the scanned port has been established
- `closed`: received `RST` flag
- `filtered`: no response (cannot determine if open or closed)

By default, `nmap` scans the most common 1000 ports. If we want to scan specify the ports we use the `-p` flag:

```
nmap -p21,22 scanme.nmap.org
```

```
root@kali:~# nmap -p21,22 scanme.nmap.org
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-10 12:29 +08
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.21s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f

PORT   STATE SERVICE
21/tcp open  ftp
22/tcp open  ssh

Nmap done: 1 IP address (1 host up) scanned in 0.81 seconds
```

To scan a range of ports:

```
nmap -p21-80 scanme.nmap.org
```

```
root@kali:~# nmap -p21-80 scanme.nmap.org
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-10 12:31 +08
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.24s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 56 closed tcp ports (reset)
PORT   STATE    SERVICE
21/tcp open     ftp
22/tcp open     ssh
25/tcp filtered smtp
80/tcp open     http

Nmap done: 1 IP address (1 host up) scanned in 3.90 seconds
```

If we want to scan all 65,535 TCP ports:
*(Note: a full TCP scan will take a long time)*

```
nmap -p- scanme.nmap.org
```

```
root@kali:~# nmap -p- scanme.nmap.org
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-10 12:32 +08
Stats: 0:21:53 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 97.64% done; ETC: 12:54 (0:00:32 remaining)
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.21s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 65529 closed tcp ports (reset)
PORT      STATE    SERVICE
21/tcp    open     ftp
22/tcp    open     ssh
25/tcp    filtered smtp
80/tcp    open     http
9929/tcp  open     nping-echo
31337/tcp open     Elite

Nmap done: 1 IP address (1 host up) scanned in 1369.31 seconds
```

Without root permissions (`sudo`), `nmap` performs TCP scans (`-sT`) instead of the default SYN scans (`-sS`). The difference between the 2 scans lie mainly with the amount of traffic generated. TCP scans forms a full three-way TCP handshake and can be easily detected by modern IDS/IPS solutions. A SYN scan on the other hand only sends the `syn` packet without establishing the handshake.

![](workshop-2-images/tcp-three-way-handshake.png)

To perform a SYN scan, we will run the command as root. We can see the difference by tracing the packets via `--packet-trace`:

```
# SYN SCAN
sudo nmap -p21 --packet-trace scanme.nmap.org
```

```
root@kali:~# sudo nmap -p21 --packet-trace scanme.nmap.org
...
SENT (0.3899s) TCP 172.20.10.9:51377 > 45.33.32.156:21 S ttl=58 id=50715 iplen=44  seq=2162333015 win=1024 <mss 1460>
RCVD (0.4143s) TCP 45.33.32.156:21 > 172.20.10.9:51377 SA ttl=64 id=0 iplen=44  seq=2428386714 win=65535 <mss 1410>
...
```

```
sudo nmap -p21 --packet-trace -sT scanme.nmap.org
```

```
root@kali:~# sudo nmap -p21 -sT --packet-trace scanme.nmap.org
...
CONN (0.3479s) TCP localhost > 45.33.32.156:21 => Operation now in progress
CONN (0.3521s) TCP localhost > 45.33.32.156:21 => Connected
...
```

UDP is a stateless protocol, which means we do not receive an acknowledgement for the target if the connection is successful. This results in a longer scan as we have to wait the timeout to be exceeded for each port. Another disadvantage is that we can only determine if a port is open if the application is configured to do so.

To perform a UDP scan, we use `-sU` flag:

```
sudo nmap -sU scanme.nmap.org
```

```
root@kali:~# sudo nmap -sU scanme.nmap.org
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-10 13:05 +08
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.25s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 999 open|filtered udp ports (no-response)
PORT    STATE SERVICE
123/udp open  ntp

Nmap done: 1 IP address (1 host up) scanned in 18.54 seconds
```

To perform a version scan, we add the `-sV` flag:

```
nmap -sV scanme.nmap.org
```

```
root@kali:~# nmap -sV scanme.nmap.org
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-10 13:11 +08
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.22s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 994 closed tcp ports (reset)
PORT      STATE    SERVICE    VERSION
21/tcp    open     tcpwrapped
22/tcp    open     ssh        OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
25/tcp    filtered smtp
80/tcp    open     http       Apache httpd 2.4.7 ((Ubuntu))
9929/tcp  open     nping-echo Nping echo
31337/tcp open     tcpwrapped
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.79 seconds
```

To perform OS detection (`-O`), version detection (`-sV`), script scanning (`-sC`) and traceroute (`--traceroute`) in one command, simply use the `-A` flag:

```
nmap -A scanme.nmap.org
```

```
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-10 13:16 +08
Nmap scan report for scanme.nmap.org (45.33.32.156)
Host is up (0.23s latency).
Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f
Not shown: 994 closed tcp ports (reset)
PORT      STATE    SERVICE    VERSION
21/tcp    open     tcpwrapped
22/tcp    open     ssh        OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 ac:00:a0:1a:82:ff:cc:55:99:dc:67:2b:34:97:6b:75 (DSA)
|   2048 20:3d:2d:44:62:2a:b0:5a:9d:b5:b3:05:14:c2:a6:b2 (RSA)
|   256 96:02:bb:5e:57:54:1c:4e:45:2f:56:4c:4a:24:b2:57 (ECDSA)
|_  256 33:fa:91:0f:e0:e1:7b:1f:6d:05:a2:b0:f1:54:41:56 (ED25519)
25/tcp    filtered smtp
80/tcp    open     http       Apache httpd 2.4.7 ((Ubuntu))
|_http-title: Go ahead and ScanMe!
|_http-favicon: Nmap Project
|_http-server-header: Apache/2.4.7 (Ubuntu)
9929/tcp  open     nping-echo Nping echo
31337/tcp open     tcpwrapped
Device type: general purpose
Running (JUST GUESSING): Linux 4.X (89%), FreeBSD 6.X (85%)
OS CPE: cpe:/o:linux:linux_kernel:4 cpe:/o:freebsd:freebsd:6.2
Aggressive OS guesses: Linux 4.19 - 5.15 (89%), FreeBSD 6.2-RELEASE (85%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 16 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 199/tcp)
HOP RTT       ADDRESS
1   5.09 ms   _gateway (172.20.10.1)
2   ...
3   54.56 ms  10.254.174.33
4   ... 15
16  280.61 ms scanme.nmap.org (45.33.32.156)

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 44.97 seconds
```

To add verbosity to your output, use the `-v` flag;

```
nmap -v scanme.nmap.org
```

```
root@kali:~# nmap -v scanme.nmap.org
Starting Nmap 7.95 ( https://nmap.org ) at 2025-09-10 13:18 +08
Initiating Ping Scan at 13:18
Scanning scanme.nmap.org (45.33.32.156) [4 ports]
Completed Ping Scan at 13:18, 0.28s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 13:18
Completed Parallel DNS resolution of 1 host. at 13:18, 0.05s elapsed
Initiating SYN Stealth Scan at 13:18
Scanning scanme.nmap.org (45.33.32.156) [1000 ports]
Discovered open port 21/tcp on 45.33.32.156
Discovered open port 80/tcp on 45.33.32.156
Discovered open port 22/tcp on 45.33.32.156
Discovered open port 31337/tcp on 45.33.32.156
Increasing send delay for 45.33.32.156 from 0 to 5 due to 69 out of 229 dropped probes since last increase.
Discovered open port 9929/tcp on 45.33.32.156
...
```

When performing network scans, you may want to save the results for future reference and analysis. Nmap can save the results to 3 formats:
- `-oN`: Normal output with `.nmap` extension
- `-oG`: Grepable output with `gnmap` extension
- `-oX`: XML output with `.xml` extension

We can also use `-oA` option to save the results in all formats:

```
nmap scanme.nmap.org -oA results
```

```
root@kali:~# ls -l | grep results
-rw-r--r-- 1 root root  461 Sep 10 13:23 results.gnmap
-rw-r--r-- 1 root root  575 Sep 10 13:23 results.nmap
-rw-r--r-- 1 root root 9931 Sep 10 13:23 results.xml
```

Bonus:

When performing scans on vulnerable machines, this is my preferred scan:

```
sudo nmap $IP -p- --min-rate=1000 -T4 --open -vv -oA enum/open-tcp-ports
```

To break the command down:
- `sudo`: superuser do, allows for SYN scans (same as `-sS`)
- `$IP`: IP of the target saves as a variable
- `-p-`: full TCP scan
- `--min-rate=1000`: send at least 1000 packets per second
- `-T4`: aggressive scan
- `--open`: only show open ports
- `-vv`: very verbose mode
- `-oA`: save the output in all 3 formats

After checking the open ports, I perform a more in-depth scan:

```
sudo nmap $IP -p <open_ports> -A -vv -oA enum/targeted-tcp-ports
```

- `-A`: OS detection (`-O`), version detection (`-sV`), script scanning (`-sC`) and traceroute (`--traceroute`)

### 5.2. Analysing Network Traffic

#### 5.2.1. Tcpdump

To capture network traffic, we will use a command-line packet analyser `tcpdump` [tcpdump](https://www.tcpdump.org/) 

To begin capturing network traffic:

```
sudo tcpdump
```

To specify interface to listen on, we can use the `-i` flag:

```
sudo tcpdump -i eth0
```

To specify a host, we use the `host` flag:

```
sudo tcpdump host scanme.nmap.org
```

To save the traffic to a `.pcap` file for further analysis (e.g. Wireshark), we use the `-w` flag:

```
sudo tcpdump host scanme.nmap.org -w captured-packets.pcap
```

#### 5.2.2. Wireshark

Wireshark is a graphical packet analyser. It has a built in sorting and filtering function for analysis on traffic.

To open wireshark, click on the top left icon in Kali Linux:

![](workshop-2-images/open-applications-view.png)

Search for wireshark and click on the application:

![](workshop-2-images/wireshark-file-explorer.png)

You should see the wireshark homepage:

![](workshop-2-images/{6BA6FE1E-B38D-4C98-A685-4F9E70DD236C}.png)

To open a `.pcap` file, click on `file` > `open` or use the keyboard shortcut `ctrl + o`:

![](workshop-2-images/open-pcap.png)

Locate your `.pcap` file in the file explorer:

![](workshop-2-images/pcap-file-explorer.png)

The `.pcap` file should now be open:

![](workshop-2-images/{A798CFE9-583C-418C-80A8-469ED3ACEE61}.png)

![](workshop-2-images/wireshark-annotate.png)

To understand packet headers, we need to understand the network layers that it corresponds to:
- **Ethernet > Data Link Layer**: sender/receiver in local network
- **IP > Network Layer**: routing across networks
- **Transport (TCP/UDP/ICMP) > Transport Layer**: data delivery between applications on different devices (ports)
- **Application (HTTP/DNS/TLS) > Application Layer**: application specific services (web browsing)
- **Payload (Data)**: actual data that is being delivered

![](workshop-2-images/Pasted%20image%2020250910152155.png
)

Wireshark display filters allow to control the type of packets are shown in the packet section. Common filters include:
- `ip.addr == 192.168.1.10`: Show packets **from or to** this IP
- `ip.src == 192.168.1.10`: Show packets **from** this IP
- `ip.dst == 192.168.1.10`: Show packets **to** this IP
- `tcp.port == 443`: Show packets using TCP port 443 (HTTPS)
- `udp.port == 53`: Show UDP DNS packets
- `http`: Show only HTTP packets
- `dns`: Show only DNS packets
- `tcp.flags.syn == 1 and tcp.flags.ack == 0`: Show **SYN packets** (start of TCP connections)
- `frame.len > 1000`: Show packets larger than 1000 bytes
- `eth.addr == aa:bb:cc:dd:ee:ff`: Filter by MAC address

After performing a nmap scan on `scanme.nmap.org`, let's use the Wireshark's display filters to get a deeper look.

To find `scanme.nmap.org` IP address:

```
dns.qry.name == scanme.nmap.org
```

```
Frame 4: 102 bytes on wire (816 bits), 102 bytes captured (816 bits)
Ethernet II, Src: 0e:6a:c4:d1:9d:64 (0e:6a:c4:d1:9d:64), Dst: PCSSystemtec_d1:f8:5d (08:00:27:d1:f8:5d)
Internet Protocol Version 4, Src: 1.1.1.1, Dst: 172.20.10.9
User Datagram Protocol, Src Port: 53, Dst Port: 39563
Domain Name System (response)
    Transaction ID: 0x7316
    Flags: 0x8180 Standard query response, No error
    Questions: 1
    Answer RRs: 1
    Authority RRs: 0
    Additional RRs: 1
    Queries
    Answers
        scanme.nmap.org: type A, class IN, addr 45.33.32.156
    Additional records
    [Request In: 1]
    [Time: 0.050835000 seconds]

```

To see all packets exchange with `45.33.32.156`:

```
ip.addr == 45.33.32.156
```

![](workshop-2-images/{D9E9095C-EC28-42C6-B7BB-035865D7434D}.png)

To see only TCP packets exchange with `45.33.32.156`:

```
ip.addr == 45.33.32.156 and tcp
```

![](workshop-2-images/{717C56E6-E94A-4C7C-A66C-06E050D51300}.png)

To see TCP packets exchange with `45.33.32.156` on port `21`:

```
ip.addr == 45.33.32.156 and tcp.port == 21
```

![](workshop-2-images/{C51C2D51-FD07-4C65-B020-9F05AE1F9FC9}.png)

## 6. References

- https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html
- https://studycorgi.com/fundamentals-of-networking/
- https://techofide.com/blogs/how-to-use-wireshark-a-full-wireshark-tutorial-techofide/
- https://en.wikipedia.org/wiki/Wireshark
- https://www.tcpdump.org/
- https://www.geeksforgeeks.org/linux-unix/tcpdump-command-in-linux-with-examples/
- https://academy.hackthebox.com
- https://www.wireshark.org/download.html
- https://www.kali.org/ 