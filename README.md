# Extended-ACLs-

# 🖧 Network Topology - Extended ACLs

این پروژه شامل یک توپولوژی شبکه در **Cisco Packet Tracer** است که در آن از **Access Control List (ACLs)** استفاده شده است.  
هدف پروژه: کنترل دسترسی بین شبکه 192.168.1.0/24 و 192.168.2.0/24 با استفاده از **Extended ACLs**.

---

## 📂 فایل‌ها
- `Extended(ACLs).pkt` → فایل اصلی شبکه برای **Cisco Packet Tracer**  
- `Extended(ACLs).png` → تصویر توپولوژی شبکه  

---

## 📌 توضیحات توپولوژی

- **Router0 (ISR4331)**
  - Gig0/0/0 → `192.168.1.1`
  - Gig0/0/1 → `192.168.2.1`

- **شبکه 1 (LAN1)**
  - Laptop0 → `192.168.1.12`
  - Laptop1 → `192.168.1.11`
  - Switch0

- **شبکه 2 (LAN2)**
  - Server0 → `192.168.2.11`
  - Server1 → `192.168.2.12`
  - Switch1

---

## ⚙️ نحوه استفاده
1. فایل `Extended(ACLs).pkt` را در نرم‌افزار **Cisco Packet Tracer** باز کنید.
2. توپولوژی شبکه همانند تصویر زیر بارگذاری خواهد شد:  

   ![Network Topology](Extended(ACLs).png)

3. وارد **CLI روتر** شوید و دستورات زیر را وارد کنید.

---

## 📜 دستورات Extended ACL

### 🔹 سناریو 
- فقط لپ‌تاپ **192.168.1.11** بتواند به سرور **192.168.2.11** دسترسی داشته باشد.  
- سایر دستگاه‌ها به این سرور دسترسی نداشته باشند.  
- دسترسی به بقیه سرورها آزاد باشد.  

### 🔹 تنظیم ACL روی روتر
```bash
enable
configure terminal

! ساخت ACL شماره 100
access-list 100 permit ip host 192.168.1.11 host 192.168.2.11
access-list 100 deny ip 192.168.1.0 0.0.0.255 host 192.168.2.11
access-list 100 permit ip any any

! اعمال ACL روی اینترفیس خروجی (LAN1 -> LAN2)
interface GigabitEthernet0/0/0
 ip access-group 100 in
exit

write memory
