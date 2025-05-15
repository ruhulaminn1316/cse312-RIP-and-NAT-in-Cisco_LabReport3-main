
---

# **RIP and NAT Configuration on Cisco Routers**

## 🎯 Objective

This guide walks you through configuring **Routing Information Protocol (RIP)** for dynamic routing and **Network Address Translation (NAT)** for IP address conversion in a Cisco router environment.

---

## ✅ Prerequisites

* Cisco Router with IOS installed
* Basic understanding of IP addressing and networking
* Access to Cisco Command Line Interface (CLI)

---

## 🛠 Procedure

### 🔁 1. RIP (Routing Information Protocol) Configuration

**Step 1: Enable RIP on the Router**

```bash
Router> enable
Router# configure terminal
Router(config)# router rip
```

**Step 2: Advertise Networks in RIP**

```bash
Router(config-router)# network 192.168.1.0
Router(config-router)# network 192.168.2.0
```

**Step 3: Use RIP Version 2 (Supports Classless Routing)**

```bash
Router(config-router)# version 2
```

**Step 4: Verify Routing Table**

```bash
Router# show ip route
```

---

### 🌐 2. NAT (Network Address Translation) Configuration

**Step 1: Define NAT Inside and Outside Interfaces**

* Inside Interface (Private Network)

  ```bash
  Router(config)# interface FastEthernet0/0
  Router(config-if)# ip nat inside
  ```

* Outside Interface (Public Network)

  ```bash
  Router(config)# interface FastEthernet0/1
  Router(config-if)# ip nat outside
  ```

**Step 2: Create Access List for Private IPs**

```bash
Router(config)# access-list 1 permit 192.168.1.0 0.0.0.255
```

**Step 3: Configure NAT with Port Address Translation (PAT)**

```bash
Router(config)# ip nat inside source list 1 interface FastEthernet0/1 overload
```

**Step 4: Check NAT Translations**

```bash
Router# show ip nat translations
```

---

## 🧠 Discussion

* **RIP (Routing Information Protocol):**
  A simple, distance-vector dynamic routing protocol that uses hop count as its metric. Best for small networks with limited routing complexity.

* **NAT (Network Address Translation):**
  A technique that translates private IP addresses to a public IP address for outbound internet traffic. PAT (Port Address Translation) allows multiple devices to share a single public IP.

---

## ✅ Conclusion

By configuring **RIP**, routers dynamically share routing information for efficient path selection. With **NAT**, internal private IPs are translated to a public IP, allowing internet access while conserving address space and enhancing security.

This dual configuration ensures proper internal routing and safe, efficient internet communication for all connected hosts.
