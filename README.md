# NETWORKWALKS-Nigel-B84-WK1-PM1-WIRESHARKLAPPRACTICE
Wireshark 
# Wireshark SOC Labs - Labs 5 to 8

Completed 4 hands-on Wireshark SOC Labs covering traffic analysis, credential exposure, brute-force detection, and VoIP.

## Work Completed

### Lab 5 - Follow TCP Stream, Part 2
- Captured live network traffic and stopped the capture to get final packet count
- Used **Follow > TCP Stream** to reconstruct the full conversation
- Found a hidden message a staff member left inside a web page on the company intranet
- Filter used: `tcp.stream eq 0`

### Lab 6 - HTTP Plain Text Credentials
- Captured a login to an old staff portal over plain HTTP
- Found username and password readable in plain text inside the packet details
- Filter used: `http.request.method == POST`
- Proved why unencrypted logins are dangerous

### Lab 7 - Catch The Brute Force Attacker
- Captured an FTP brute-force attack
- Identified the attacker IP from hundreds of failed login attempts in a short time
- Analyzed the pattern: same destination, same port, many different passwords
- Filters used: `ftp` , `ip.src == [Attacker-IP]`
- Mitigation: Block IP, rate-limiting, account lockout, strong passwords, MFA

### Lab 8 - VoIP Call Analysis
- Captured a VoIP call
- Found call setup with: `sip.Request.Method == INVITE`
- Caller identified from `From:` header in SIP
- Codec: **G.711 PCMU - Payload Type 0**
- Playback: `Telephony > VoIP Calls > Play Streams` to listen to RTP audio

## Lessons Learnt

1. **If it's not encrypted, Wireshark can read it** - HTTP passwords, TCP messages, even phone calls.
2. **Attacks leave a pattern** - Brute force is easy to spot when you filter by IP and failed attempts.
3. **SIP sets up the call, RTP carries the voice** - Both need SRTP + TLS (SIPS on port 5061) to be secure.
4. **Good analysis = Capture > Stop > Filter > Follow Stream > Find Evidence**

## Tools Used
- Wireshark
- NetworkWalks SOC Labs
- PCAP / Live Capture

## Key Takeaway
Wireshark proves one rule: If traffic isn't encrypted, anyone on the network can capture, read, and replay it.![Uploading 17636.jpg…]()
<img width="4160" height="3120" alt="17610" src="https://github.com/user-attachments/assets/ece6956c-4505-4440-85ee-47116c90cb86" />
