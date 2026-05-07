# 🌐 Networking Fundamentals

## What Is Networking? (The Big Picture)

A network is simply devices talking to each other — sharing files, accessing the internet, sending emails. To do that reliably, networking relies on four things:

1. **Addresses** — where is the data going? *(IP & MAC addresses)*
2. **Pathways** — how does it get there? *(cables, Wi-Fi, routers)*
3. **Rules** — how do devices agree to communicate? *(protocols)*
4. **Security** — is it safe? *(firewalls, encryption, authentication)*

> *Think of a network like a city's postal system. You need addresses (IPs), roads (cables), sorting offices (routers/switches), and rules (protocols) to make sure every letter (data packet) reaches the right door.*

---


# FOUNDATIONS

---

## 1. Network Components — The Building Blocks

Every network is made up of key hardware. Understanding what each device does — and at which layer — is fundamental.

| Device | OSI Layer | What It Does |
|---|---|---|
| **Hub** | 1 | Repeats signal to ALL devices — no intelligence, creates collisions |
| **Switch** | 2 | Sends data ONLY to the right device using MAC addresses |
| **Router** | 3 | Connects different networks using IP addresses |
| **Wireless Access Point (WAP)** | 1–2 | Radio bridge — lets Wi-Fi devices join a wired network |
| **Firewall** | 3–7 | Enforces traffic rules — blocks/allows based on policy |
| **Load Balancer** | 4–7 | Distributes traffic across multiple servers to prevent overload |
| **Proxy Server** | 7 | Acts as a middleman — fetches content on your behalf |
| **IDS** | Passive monitor | Detects and *alerts* on suspicious traffic |
| **IPS** | Active monitor | Detects and *blocks* suspicious traffic automatically |
| **NAS** | Storage | Shared file storage accessible over the network |
| **Client** | — | Any device a user operates (laptop, phone, tablet) |
| **Server** | — | Provides resources to the network (email, files, web) |

> **Core rule:** Switches use MAC addresses. Routers use IP addresses. This distinction underpins almost everything else in networking.

---

## 2. Network Sizes

Networks are categorised by geographic coverage:

| Type | Full Name | Range | Real-World Example |
|---|---|---|---|
| **PAN** | Personal Area Network | ~10 feet | Bluetooth headphones to phone |
| **LAN** | Local Area Network | ~100 metres | Home Wi-Fi, office, school |
| **CAN** | Campus Area Network | Several miles | University campus, business park |
| **MAN** | Metropolitan Area Network | Up to ~25 miles | City-wide council/hospital network |
| **WAN** | Wide Area Network | Global | The internet itself |

> *A PAN is your driveway. A LAN is your street. A CAN is your neighbourhood. A MAN is your city's road network. A WAN is the entire motorway system.*

---

## 3. The OSI Model — The 7-Layer Framework

The OSI (Open Systems Interconnection) model is a framework that describes how data travels across a network. At beginner level it's a memorisation task. At intermediate level it becomes your primary **diagnostic and troubleshooting tool**.

### The 7 Layers

| Layer | Name | Job | Data Unit | Key Protocols/Devices |
|---|---|---|---|---|
| 7 | **Application** | User-facing apps (browser, email) | Data | HTTP, HTTPS, DNS, FTP, SMTP |
| 6 | **Presentation** | Translates, encrypts, compresses data | Data | TLS/SSL, JPEG, ASCII, MP4 |
| 5 | **Session** | Starts, maintains, ends conversations | Data | NetBIOS, H.323 |
| 4 | **Transport** | Reliable/unreliable delivery, uses ports | Segments/Datagrams | TCP, UDP |
| 3 | **Network** | IP addresses and routing between networks | Packets | IP, ICMP, Routers |
| 2 | **Data Link** | MAC addresses, delivers data on one hop | Frames | Switches, Ethernet, ARP |
| 1 | **Physical** | Raw bits — voltage, light, radio waves | Bits | Cables, Hubs, Wi-Fi signals |

**Memory trick (top to bottom):** *"All People Seem To Need Data Processing"*
→ Application, Presentation, Session, Transport, Network, Data Link, Physical

### Encapsulation & Decapsulation

When data is **sent**, each layer wraps it with a header (encapsulation — going DOWN):
```
[App Data]                            ← Layer 7
[TCP header + Data]       = Segment   ← Layer 4
[IP header + Segment]     = Packet    ← Layer 3
[Ethernet header + Packet]= Frame     ← Layer 2
[Bits on the wire]                    ← Layer 1
```
When data is **received**, each layer removes its header (decapsulation — going UP).

> *"Sending a letter." You write it (L7), put it in an envelope (L6), address it (L3), hand it to the post office (L2), it travels physically (L1). The receiver reverses the process.*

### OSI as a Troubleshooting Tool

When something breaks, work layer by layer upward:

| Layer | Question | Example Problem |
|---|---|---|
| 1 | Is there a physical signal? | Broken cable, no link light |
| 2 | Are frames being formed correctly? | MAC table issue, duplex mismatch |
| 3 | Is the IP/routing correct? | Wrong subnet, missing default gateway |
| 4 | Is the right port open? | Firewall blocking TCP 443 |
| 5–7 | Is the application behaving? | DNS failure, expired certificate |

---
