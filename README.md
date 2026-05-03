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