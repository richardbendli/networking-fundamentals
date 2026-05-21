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

## 4. IP Addressing

### IPv4 Basics

Written in **dotted decimal notation**: `192.168.1.10`
- 32-bit address → ~4.3 billion possible addresses
- Split into: **Network portion** (which network) + **Host portion** (which device)

### IPv4 Address Classes

| Class | Range | Default Mask | Hosts Per Network |
|---|---|---|---|
| A | 1–126 | /8 | ~16 million |
| B | 128–191 | /16 | ~65,000 |
| C | 192–223 | /24 | 254 |
| D | 224–239 | — | Multicast |
| E | 240–255 | — | Experimental |

> *Classes are mostly obsolete — replaced by CIDR — but you'll still see this terminology in documentation.*

### Private IP Ranges (RFC 1918)

These addresses are used inside homes and offices. They are **never routed on the public internet**.

| Range | Common Use |
|---|---|
| `10.0.0.0 – 10.255.255.255` | Large organisations |
| `172.16.0.0 – 172.31.255.255` | Medium networks |
| `192.168.0.0 – 192.168.255.255` | Home networks |

### Special Reserved Addresses

| Address | Purpose |
|---|---|
| `127.0.0.1` | Loopback — your device talking to itself |
| `169.254.x.x` | APIPA — auto-assigned when DHCP fails |
| `0.0.0.0` | Unspecified / default route |
| `255.255.255.255` | Limited broadcast (all devices on local subnet) |

### IPv6 — Why It Exists

IPv4 only has ~4.3 billion addresses. IPv6 fixes the exhaustion problem:
- **128-bit addresses** → 340 undecillion addresses
- Written in **hexadecimal with colons**: `2001:0db8:85a3::8a2e:0370:7334`
- Shorthand: consecutive zero groups → `::` (used only once per address)
- **No broadcasts** — more efficient
- Devices can assign themselves addresses automatically (**SLAAC**)

| Feature | IPv4 | IPv6 |
|---|---|---|
| Address length | 32-bit | 128-bit |
| Notation | Dotted decimal | Hex with colons |
| Address space | ~4.3 billion | 340 undecillion |
| Broadcasts | Yes | No (uses multicast) |
| Auto-configuration | DHCP | SLAAC |

---

## 5. Subnetting — Dividing a Network

**Subnetting** means splitting one large network into smaller, more manageable pieces.

### Why Subnet?
- **Security** — isolate departments from each other
- **Performance** — smaller broadcast domains = less noise
- **Organisation** — logical groupings match business structure
- **Efficiency** — assign only the IPs each group needs

### Subnet Mask

Tells your device which part of an IP is the network and which is the host.
- `/24` = first 24 bits are network → 256 total IPs, 254 usable
- The smaller the CIDR number, the larger the network

### Subnetting Reference Table

| CIDR | Subnet Mask | Total IPs | Usable IPs |
|---|---|---|---|
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 8 | 6 |
| /30 | 255.255.255.252 | 4 | 2 |

> *Usable IPs = `2ʰ - 2` (h = host bits; subtract 2 for network address and broadcast address)*

### VLSM — Variable Length Subnet Masking

Real networks have departments of different sizes. VLSM lets you assign right-sized subnets:
- Sales (50 users) → `/26` (62 usable)
- HR (10 users) → `/28` (14 usable)
- WAN link between two routers → `/30` (2 usable — exactly right!)

> *Subnetting is cutting a pizza into slices. VLSM means cutting unequal slices — giving a bigger piece to whoever needs more.*

> **Always** start subnetting from the **largest** requirement and work down to smallest.

---

## 6. TCP vs. UDP — Two Ways to Send Data

Both operate at **Layer 4 (Transport)** of the OSI model.

### TCP — Transmission Control Protocol

- **Connection-oriented** — establishes a connection before sending data
- **Reliable** — guarantees delivery, sequencing, and error checking
- **Uses the Three-Way Handshake:**
  1. **SYN** → "Hello, I want to connect"
  2. **SYN-ACK** → "Hello back, I'm ready"
  3. **ACK** → "Great, let's go"
- **Windowing** — dynamically adjusts how much data is sent at once based on network conditions
- **Used for:** Web browsing, email, file downloads, anything where data loss is unacceptable

### UDP — User Datagram Protocol

- **Connectionless** — no handshake, just sends
- **Unreliable** — no delivery guarantee ("fire and forget")
- **Faster** — less overhead
- **Used for:** Live video/audio, gaming, VoIP, DNS lookups — where speed matters more than perfection

### TCP vs. UDP Comparison

| Feature | TCP | UDP |
|---|---|---|
| Connection | Required (3-way handshake) | Not required |
| Reliability | Guaranteed | Not guaranteed |
| Ordering | Yes — sequence numbers | No |
| Speed | Slower | Faster |
| Error checking | Yes | Optional |
| Use cases | Web, email, files | Video, gaming, VoIP |

> *TCP is like sending a parcel with a signature required — you know it arrived. UDP is like posting leaflets — fast, no confirmation.*

---
