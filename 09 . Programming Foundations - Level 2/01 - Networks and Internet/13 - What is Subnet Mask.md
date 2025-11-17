---
DATE: 2025-08-26T07:52:00
DONE: true
Name: Foundation 2
---



#### **A subnet mask** 
is a 32-bit number that divides an IP address into two parts: the **network portion** and the **host portion**. The 1s in the subnet mask indicate the network address portion, while the 0s represent the host portion.

**Simple Analogy**: Think of it like a postal address:
- **Network portion** = Your street name (identifies the neighborhood)
- **Host portion** = Your house number (identifies specific device)

---

## 🎯 What is Subnetting?

**Subnetting** is the practice of dividing a large network into two or more smaller networks (subnets). This creates a hierarchy that makes network management more efficient and secure.

### Why We Use Subnetting:
1. **Improved Security** - Isolate different parts of the network
2. **Reduced Network Traffic** - Limit broadcast domains
3. **Better Organization** - Logical grouping of devices
4. **Efficient IP Address Planning** - Optimize IP address allocation
5. **Enhanced Routing Efficiency** - Faster data packet delivery

---

## 🔢 How Subnet Masks Work

### Common Subnet Mask Examples:

| Subnet Mask | CIDR Notation | Binary Representation | Available Hosts |
|------------|---------------|----------------------|-----------------|
| 255.255.255.0 | /24 | 11111111.11111111.11111111.00000000 | 254 |
| 255.255.255.128 | /25 | 11111111.11111111.11111111.10000000 | 126 |
| 255.255.255.192 | /26 | 11111111.11111111.11111111.11000000 | 62 |
| 255.255.255.224 | /27 | 11111111.11111111.11111111.11100000 | 30 |
| 255.255.0.0 | /16 | 11111111.11111111.00000000.00000000 | 65,534 |

### Understanding CIDR Notation:

CIDR (Classless Inter-Domain Routing) notation uses a slash followed by a number (e.g., /24). This number represents how many consecutive 1s are in the subnet mask when converted to binary.

**Example**: 
- IP Address: `192.168.1.100/24`
- Subnet Mask: `255.255.255.0`
- Network Portion: `192.168.1` (first 24 bits)
- Host Portion: `.100` (last 8 bits)

---

## 💡 Real-World Example

### Home Network Scenario:
```
Router IP: 192.168.1.1
Subnet Mask: 255.255.255.0 (/24)

Valid IP Range: 192.168.1.1 - 192.168.1.254
- Network Address: 192.168.1.0 (cannot be assigned)
- Broadcast Address: 192.168.1.255 (cannot be assigned)
- Usable IPs: 192.168.1.1 - 192.168.1.254 (254 devices)
```

### Corporate Network with Departments:
```
Company Network: 192.168.0.0/16

Subnets:
├─ Sales Department: 192.168.1.0/24 (254 hosts)
├─ IT Department: 192.168.2.0/24 (254 hosts)
├─ HR Department: 192.168.3.0/24 (254 hosts)
└─ Guest Network: 192.168.100.0/24 (254 hosts)
```

---

## 🔍 How Routers Use Subnet Masks

Routers use subnet masks to sort data packets into subnetworks and route them to the right place. When a device sends data:

1. **Source device** checks if destination is on the same subnet
2. **Subnet mask** helps determine: same network or different network?
3. If **same network**: Direct communication
4. If **different network**: Send to router/gateway

---

## 🎓 Key Concepts to Remember

### Network Address vs Host Address:
- **Network Address**: Identifies which network a device belongs to
- **Host Address**: Identifies the specific device within that network
- **AND Operation**: Subnet mask uses logical AND with IP address to extract network address

### Subnet Mask Rules:
1. Always continuous 1s followed by continuous 0s
2. More 1s = smaller subnet (fewer hosts)
3. More 0s = larger subnet (more hosts)
4. First address (all 0s in host) = Network Address
5. Last address (all 1s in host) = Broadcast Address

---



**الSubnet Mask** هو رقم 32 بت يقسم عنوان IP إلى جزئين:
- **جزء الشبكة** (Network) - يحدد الشبكة
- **جزء الجهاز** (Host) - يحدد الجهاز داخل الشبكة

**الSubnetting** هو تقسيم الشبكة الكبيرة إلى شبكات صغيرة:
- ✅ يزيد من الأمان (Security)
- ✅ يقلل من حركة المرور (Traffic)
- ✅ ينظم الشبكة بشكل أفضل
- ✅ يحسن استخدام عناوين IP

**مثال بسيط**:
```
Subnet Mask: 255.255.255.0
معناها: أول 24 بت للشبكة، آخر 8 بت للأجهزة
عدد الأجهزة الممكنة: 254 جهاز
```

---

## 🔗 Quick Reference

**Most Common Subnet Masks:**
- `255.255.255.0` (/24) → Home/Small Office (254 hosts)
- `255.255.255.128` (/25) → Small Department (126 hosts)
- `255.255.0.0` (/16) → Large Organization (65,534 hosts)
- `255.0.0.0` (/8) → Massive Network (16,777,214 hosts)

**Remember**: The subnet mask determines how many devices can exist on your network!