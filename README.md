# NetPractice

**NetPractice** is a 42 school project where I learned the basics of computer networking through interactive exercises.  
The goal of the project is to understand how TCP/IP addressing works and how to configure small-scale networks so that they become functional.

## 📌 Project Overview
- The project comes with an interactive web interface (`index.html`) where I had to solve networking problems step by step.  
- There are **10 levels**, each with a broken network that needs to be fixed.  
- The main tasks involved:
  - Assigning correct IP addresses.  
  - Setting up subnet masks.  
  - Configuring routes so devices could communicate properly.  
- The interface provides logs and real-time feedback, which helped me debug my configurations.  
- Once solved, I exported the solutions using the **[Get my config]** button and submitted them (1 file per level).

## 🎯 What I Learned
- How IP addressing and subnetting work.  
- How to configure networks with hosts, routers, and subnets.  
- Hands-on practice in solving real networking problems.  
- Built a solid foundation for more advanced networking and system administration projects.

## ✅ Evaluation
- During the defense, I had to solve **3 random levels (from 6 to 10)** within 15 minutes.  
- No external tools were allowed (except for a simple calculator like `bc`).  

## 🚀 Takeaway
This project really helped me get more comfortable with networking fundamentals, especially subnetting and IP routing, which are essential skills for both system administration and more advanced network setups.

---

## 🌐 Networking Basics (Notes)

### IP Address
- IPv4 addresses are composed of **4 octets** (e.g., `192.168.1.1`).
- Each address has a **network portion** and a **host portion** (defined by the subnet mask).
- The **first address** in a subnet is reserved as the **network address**.  
- The **last address** is reserved as the **broadcast address**.

### Subnet
- A subnet is a subdivision of a network that shares a common, identifiable network address.
- Example: `192.168.1.0/24` → `/24` means the first 24 bits identify the network, the last 8 bits identify hosts.
- Subnets allow determining whether a host belongs to a given network.

### 💡 Tips on how to use Linux `bc`
#### CIDR (Classless Inter-Domain Routing)
- CIDR notation indicates how many bits are used for the network portion.  
- Example: `255.255.255.0` in binary → `11111111.11111111.11111111.00000000` = `/24`.  
- Quick check in Linux with `bc`:
  ```sh
  $ bc
  obase=2
  255
  11111111
  ```

#### Calculating IP ranges
- Formula: `2^(32 - CIDR)` = total number of addresses in the subnet.  
- Subtract 2 to find usable host addresses (network & broadcast are reserved).  
  ```sh
  $ bc
  2^(32-24)
  256
  ```
- `/24` → `2^(32-24) = 256` total → `254` usable hosts.  
- `/30` → `2^(32-30) = 4` total → `2` usable hosts.  
- `/18` → `2^(32-18) = 16384` total → `16382` usable hosts.  

👉 This helps quickly estimate how large or small a subnet is.

### Communication Rules
- Every client IP must be **unique** within the network.
- Clients can only communicate **locally** if they are within the same subnet (CIDR range).
- All devices on the same LAN (e.g., connected to the same switch) must share the same **subnet mask** so they can identify each other as local.

### Routing
- Routing tables match **destination IPs**, not sources.
- Each entry defines **where to send packets** (next hop or interface).
- The **default route** (`0.0.0.0/0`) is used when no specific route matches.

### Interfaces
- Interfaces are physical or virtual network ports (e.g., `eth0`, `wlan0`) where IPs are assigned.
- They represent where data is sent and received.

### Route Format
- General format:  
  ```
  Destination (CIDR) => Next Hop (Gateway IP / Interface)
  ```
  Example:  
  ```
  192.168.1.0/24 => 192.168.1.1
  0.0.0.0/0      => 10.0.0.1   (default route)
  ```

---

## 📅 Project Notes
I finished this project on **August 7, 2025**, using **subject version 4.0** and **NetPractice 1.6**. After practicing the given exercises, I realized there is often a pattern: each exercise is very similar each time you refresh the page, with only small changes. [Here](https://github.com/podefteza/NetPractice/blob/main/Levels%201%20to%2010.pdf) are my notes on each level.

👉 Keep in mind, however, that the **goal of this project is to understand how networks work**, not to memorize the exercises, but by recognizing these patterns, it becomes easier to spot what is wrong (IPs, routes, or masks) and apply the right fix.
