# OSCP-Prep
# OSCP Preparation Guide: Checklists, Timetable, Machines, Tools & Techniques

Hello! Below is a comprehensive OSCP (Offensive Security Certified Professional) preparation guide compiled from various sources like GitHub repositories, Medium articles, Reddit, and OSCP-related websites. I've included TJ Null's OSCP-like machines list, additional machines from other platforms, checklists, a daily timetable, and detailed tools & techniques.

This guide is in clean Markdown format (fully in English). You can easily copy-paste it into a Markdown editor (like Obsidian, Notion, or Typora) or convert it to PDF using tools like Pandoc or online converters.

**Note:** This guide is updated for the 2025 context. Always verify the latest OSCP course materials and exam rules on the official OffSec website. Practice on platforms like HTB, TryHackMe, VulnHub, and Proving Grounds.

## 1. Daily Timetable

A structured daily routine is essential for OSCP preparation. The sample below is based on experiences from people who passed OSCP and Medium articles. It's designed for people with a full-time job, but you can adjust it. Aim for 4–6 hours of study daily, with more on weekends. Total preparation time: 3–6 months.

### Sample Daily Routine (Weekday)

| Time Slot              | Activity                  | Details                                                                 |
|-----------------------|---------------------------|-------------------------------------------------------------------------|
| 10:30 AM              | Wake Up & Morning Routine | Hygiene, meditation, or light exercise (30 mins)                         |
| 11:00 AM              | Breakfast                 | Healthy meal                                                            |
| 11:30 AM – 1:00 PM     | Theory Study              | Read PEN-200 materials, watch videos, take notes (networking, enumeration, web attacks) |
| 1:00 PM – 1:30 PM      | Break                     | Walk, stretch, relax to avoid burnout                                   |
| 1:30 PM – 2:30 PM      | Practical Labs            | Work on OSCP labs, HTB/TryHackMe machines, focus on new techniques      |
| 2:30 PM – 3:00 PM      | Lunch                     | Quick meal                                                              |
| 3:00 PM – 11:00 PM     | Work/Other Commitments    | Job or daily tasks                                                      |
| 11:00 PM onwards      | Relaxation & Sleep        | Wind down; aim for 7–8 hours of sleep. Quick 30-min review if energized |

### Weekend Schedule (Saturday/Sunday)

- Sleep in for recovery.
- 11:00 AM – 1:00 PM: Theory review.
- 1:00 PM – 5:00 PM: Intensive labs (solve 2–3 machines, write reports).
- Evening: Free time or light reading (blogs, forums).
- Total: 6–8 hours of study per day.

**Timetable Tips:**
- Track progress in a journal (Notion, Obsidian).
- Use Pomodoro: 25 mins study + 5 mins break.
- If stuck, switch topics.
- Weekly goal: Complete 5–10 machines and review notes.

## 2. Checklists

Enumeration and a systematic approach are key in OSCP. Below are checklists compiled from GitHub repos (e.g., OSCP-Checklist-Cheatsheet 2024) and community sources.

### General Checklist (Before Starting Any Machine)
1. Authenticate to BloodHound with credentials.
2. Quick BloodHound enumeration.
3. Claim all flags and take screenshots.
4. Check anonymous/guest SMB access on all IPs.
5. Attack DC even without credentials.
6. Try default credentials (e.g., offsec:lab).
7. Run thorough enumeration even with local admin (WinPEAS/LinPEAS).
8. Re-enumerate with new credentials.
9. Try username = password.
10. Use `nxc smb IP -u creds.txt -p creds.txt --no-bruteforce`.
11. Check shares with guest/anonymous access.
12. Run rpcdump/enum4linux with credentials.
13. Kerbrute user enum: `/Tools/kerbrute userenum -d domain --dc IP usernames.txt`.
14. AS-REP roasting: `impacket-GetNPUsers domain/ -usersfile creds.txt -request -outputfile hashes`.
15. UDP scan: `nmap -sUV --top-ports 1000 IP`.
16. Re-run PEAS with higher privileges.
17. SMB connect: `impacket-smbclient domain/guest@IP`.
18. **Try Harder:** Repeat enumeration if stuck.

### Web Application Checklist

#### Pre-Authentication
1. Disable ad-blockers and custom user agents.
2. Find web servers: `nmap -sV -p 80,443,8080,... --script http-title IP`.
3. Identify tech stack: `whatweb URL` or Wappalyzer.
4. Check via web-check.as93.net.
5. Directory enumeration: `feroxbuster -u URL -w raft-large-files.txt`.
6. PDF search: `feroxbuster -x pdf | grep '\.pdf$'`.
7. Scan with Nessus, Nuclei, Nikto, Sn1per.
8. Use DevTools for network inspection.
9. Run Burp Suite scan.
10. Subdomain enum: `subfinder | httpx`.
11. Build directory list in Burp and feed to feroxbuster.
12. Search exploits: searchsploit, Sploitus, CVEMap.
13. Test LFI/RFI.
14. Proceed to login brute-forcing.
15. Check for exposed Git repos.
16. **Try Harder.**

#### Directory Enumeration
1. Check robots.txt and sitemap.xml.
2. feroxbuster with extensions: `-x php,bash,txt,bak`.
3. Go deeper: `--depth 2 --filter-status 404`.
4. Use Katana: `katana -u URL`.
5. Export from Burp to feroxbuster.
6. Look for hidden files/directories.
7. **Try Harder.**

#### Login Checklist
1. Try empty credentials.
2. Username as password.
3. Default credential search.
4. Brute-force with small wordlists.
5. Fuzz special characters.
6. Attempt login bypasses.
7. Use Cewl-generated wordlists.
8. Check for account lockout.
9. Analyze error messages.
10. **Try Harder.**

### Network & Port Scan Checklist
- Passive: `netdiscover -p`, tcpdump, Responder.
- Active: `netdiscover`, nmap ping sweep, fping.
- Ports: masscan common ports, nmap full `-p-`.
- UDP: `nmap -sU --top-ports=100`.
- Protocols: `nmap -sUV -F`.
- **Try Harder.**

### Active Directory Checklist
1. Define primary target.
2. Use SharpHound/BloodHound.
3. Repeat per user.
4. Kerberos attacks (Kerberoasting, AS-REP).
5. DCSync/DCShadow.
6. Run Responder.
7. enum4linux.
8. Check Sysvol shares.
9. Review permissions after psexec.
10. **Try Harder.**

## 3. Machine Practice List

Solve 50–100 machines for OSCP. Start with TJ Null's list (most OSCP-like). I've categorized by difficulty and platform.

### TJ Null's OSCP-Like Machines (Ordered by Difficulty)

#### Easy
| Machine      | Platform | Notes                  |
|--------------|----------|------------------------|
| Active       | Windows  | AD basics              |
| Armageddon   | Linux    | Web exploits           |
| Bashed       | Linux    | Simple priv esc        |
| Bastion      | Windows  | SMB                    |
| Beep         | Linux    | VoIP                   |
| Blocky       | Linux    | Minecraft-related      |
| Blunder      | Linux    | CMS                    |
| Bounty       | Windows  | WebDav                 |
| Delivery     | Linux    | Ticket system          |
| Devel        | Windows  | FTP                    |
| Doctor       | Linux    | Splunk                 |
| Forest       | Windows  | AD                     |
| FriendZone   | Linux    | SMB                    |
| Frolic       | Linux    | PlayCMS                |
| Grandpa      | Windows  | Old IIS                |
| Granny       | Windows  | WebDav                 |
| Horizontall  | Linux    | Laravel                |
| Irked        | Linux    | IRC                    |
| Jerry        | Windows  | Tomcat                 |
| Knife        | Linux    | PHP                    |
| Love         | Windows  | Voting system          |
| Legacy       | Windows  | SMB                    |
| Luanne       | Other    | NetBSD                 |
| Mirai        | Linux    | IoT                    |
| Networked    | Linux    | Upload                 |
| Nibbles      | Linux    | Nibbleblog             |
| Omni         | Windows  | IoT                    |
| OpenAdmin    | Linux    | OpenNetAdmin           |
| Optimum      | Windows  | HttpFileServer         |
| Previse      | Linux    | Site script            |
| Postman      | Linux    | Redis                  |
| Remote       | Windows  | Umbraco                |
| ScriptKiddie | Linux    | msfconsole             |
| Sense        | FreeBSD  | pfSense                |
| ServerMon    | Windows  | -                      |
| Shocker      | Linux    | Shellshock             |
| Sunday       | Solaris  | Finger                 |
| Support      | Windows  | SupportDesk            |
| Swagshop     | Linux    | Magento                |
| Traverxec    | Linux    | nostromo               |
| Tabby        | Windows  | Tomcat                 |
| Valentine    | Linux    | Heartbleed             |

#### Medium
| Machine       | Platform | Notes             |
|---------------|----------|-------------------|
| Bastard       | Windows  | Drupal            |
| Chatterbox    | Windows  | AChat             |
| Cronos        | Linux    | DNS               |
| Forge         | Linux    | SSL               |
| Fuse          | Windows  | Printer           |
| Haircut       | Linux    | Curl              |
| Intelligence  | Windows  | AD                |
| Jarvis        | Linux    | MySQL             |
| Magic         | Linux    | Magick            |
| Mango         | Linux    | NoSQL             |
| Nineveh       | Linux    | Secure notes      |
| Node          | Linux    | Node.js           |
| Ophiuchi      | Linux    | YAML              |
| Passage       | Linux    | USBCreator        |
| Pit           | Linux    | SNMP              |
| Poison        | Linux    | VNC               |
| Popcorn       | Linux    | Torrent           |
| Ready         | Linux    | GitLab            |
| Seal          | Linux    | GitLab            |
| SecNotes      | Windows  | IIS               |
| Shibboleth    | Linux    | IPMI              |
| Silo          | Windows  | Oracle            |
| SolidState    | Linux    | James mail        |
| SneakyMailer  | Linux    | PHP mail          |
| Tartarsauce   | Linux    | tar wp            |
| Worker        | Windows  | Azure DevOps      |
| Writer        | Linux    | Apache            |

#### Hard & Insane
(Refer to TJ Null's Google Sheet for the complete latest list: https://docs.google.com/spreadsheets/d/1dwSMIAPIam0PuRBkCiDI88pU3yzrqqHkDtBngUHNCw8)

### Additional Recommended Machines
- HTB: Blue, Canape, Help, Joker, Lame, RedCross
- VulnHub: Bob, Brainpan, GoldenEye, NullByte, Pluck, Sedna
- TryHackMe: Alfred, Blue, Brainstorm, Corp, HackPark, Ignite, Kenobi, Skynet, Steel Mountain, Thompson

**Machine Tips:**
- Start with Easy → Medium → Hard.
- Write a report after every machine.
- Total goal: 50–80 machines (HTB VIP recommended).

## 4. Tools and Techniques

Focus on manual tools; Metasploit is allowed only on one machine in the exam.

### Approved Tools
#### Note-Taking
- Obsidian, OneNote, Joplin

#### Enumeration
- AutoRecon, nmapAutomator, RustScan

#### Web
- DirSearch, Gobuster, ffuf, Nikto, feroxbuster

#### Networking
- Impacket

#### Wordlists
- SecLists

#### Payloads
- MSFVenom, Reverse Shell Generator

#### Priv Esc
- LinPEAS, WinPEAS, GTFOBins, PowerUp

#### Password Cracking
- Hashcat, John the Ripper, Hydra

#### Buffer Overflow
- VulnServer, Immunity Debugger

### Key Techniques
- **Enumeration:** Nmap (`-sC -sV`), enum4linux, smbclient.
- **Web Attacks:** Burp Suite (XSS, SQLi, LFI), feroxbuster.
- **Priv Esc:** Kernel exploits, sudo abuse, scheduled tasks.
- **AD Attacks:** Kerberoasting, AS-REP roasting, BloodHound.
- **Pivoting:** SSH tunneling, Chisel, Socat.
- **Buffer Overflow:** pattern_create, mona.py.
- **Reporting:** Use OSCP template with screenshots and commands.

**Final Tips:** Use cheat sheets (HackTricks, PayloadsAllTheThings). Watch Ippsec videos only when stuck. Stay healthy and consistent.

Good luck with your OSCP journey! Try harder! 
