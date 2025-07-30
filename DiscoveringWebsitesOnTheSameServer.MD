# Discovering Websites On The Same Server: tesla.com
**Thực hiện:** Lê Thị Mỹ Tiên  
**Cập nhật lần cuối:** 29/07/2025  

---

## 1. Mục lục
- Mục tiêu thăm dò
- Công cụ thực hiện
- Các bước thực hiện
- Kết luận

---

## 2. Nội dung

### 2.1 Mục tiêu
Việc tìm các website khác cùng nằm trên một máy chủ thường nhằm các mục đích như:
- Mở rộng phạm vi kiểm thử và tìm lỗ hổng bảo mật (pentest).
- Phân tích tối ưu hóa công cụ tìm kiếm để phát hiện mạng site vệ tinh hoặc hoạt động của đối thủ.
- Hỗ trợ quản trị hệ thống và điều tra sự cố khi nhiều website dùng chung tài nguyên.
- Phục vụ thu thập thông tin (OSINT) để có thêm dữ liệu liên quan đến tổ chức hay cá nhân.

---

### 2.2 Công cụ
- `nslookup`
- Reverse IP Lookup ([viewdns.info](https://viewdns.info))
- `subfinder`
- `amass (enum -passive)`
- `grep` / lọc file

---

### 2.3 Các bước thực hiện

#### Giai đoạn 1: Initial Reconnaissance

#### **Bước 1: Thu thập IP**
Lệnh:

```bash
nslookup tesla.com
```

Kết quả:

```
Server:         192.168.198.2
Address:        192.168.198.2#53
Non-authoritative answer:
Name:   tesla.com
Address: 2.18.50.207
Name:   tesla.com
Address: 23.40.100.207
Name:   tesla.com
Address: 2.18.54.207
Name:   tesla.com
Address: 2.18.55.207
Name:   tesla.com
Address: 2.18.53.207
Name:   tesla.com
Address: 2.18.51.207
Name:   tesla.com
Address: 2.18.49.207
Name:   tesla.com
Address: 23.7.244.207
Name:   tesla.com
Address: 2.18.48.207
Name:   tesla.com
Address: 2.18.52.207
```

Nhận xét:
- Lệnh `nslookup tesla.com` trả về nhiều địa chỉ IP khác nhau, cụ thể các dải `2.18.x.x` và `23.x.x.x`.
- Các dải IP này thuộc về **Akamai Technologies (CDN)**, không phải hạ tầng trực tiếp của Tesla.
- Việc xuất hiện nhiều IP cho thấy Tesla đang sử dụng **CDN** kết hợp cơ chế **load balancing** để phân phối lưu lượng.

---

#### **Bước 2: Tra cứu các domain cùng IP (Reverse IP Lookup)**

**Bước 2.1**: Reverse lookup từng IP:

```bash
nslookup 2.18.50.207
nslookup 23.40.100.207
nslookup 2.18.54.207
```

Kết quả:

```
207.50.18.2.in-addr.arpa name = a2-18-50-207.deploy.static.akamaitechnologies.com.
207.100.40.23.in-addr.arpa name = a23-40-100-207.deploy.static.akamaitechnologies.com.
207.54.18.2.in-addr.arpa name = a2-18-54-207.deploy.static.akamaitechnologies.com.
```

**Bước 2.2**: Sử dụng công cụ online:

- Truy cập [viewdns.info/reverseip](https://viewdns.info/reverseip)
- Kết quả: **Các IP 2.18.50.207, 23.40.100.207… chỉ có 1 tên miền được lưu trữ: tesla.com**.

Nhận xét:
- Tesla đang sử dụng Akamai CDN.
- Các IP này thuộc về Akamai Technologies, không phải server gốc của Tesla.

---

#### **Bước 3: Identify CDN/Protection**

![IdentifyCDN](https://github.com/My-Tien1611/InformationGathering_LeThiMyTien/blob/68a3864420012e3c254fd3ba01a8c1da6c9f4987/IdentifyCDN_Protection.webp)

- Server: `AkamaiGHost` → Xác nhận Tesla dùng Akamai CDN
- Không phát hiện Cloudflare.
- Response headers chỉ từ **edge servers**.

---

#### **Bước 4: Passive Recon bằng Subdomain Enumeration**

Dùng CLI tool:

```bash
subfinder -d tesla.com -silent > subdomains.txt
amass enum -passive -d tesla.com >> subdomains.txt
```

![no_cdn](https://github.com/My-Tien1611/InformationGathering_LeThiMyTien/blob/97181ae0fbad5105fea496a5dccdb789a63824ff/Nocdn.jpg)

Kết quả:
- File `no_cdn.txt` trống nghĩa là:
  - Tất cả subdomain trong `subdomains.txt` đều resolve ra IP thuộc Akamai CDN.
  - Không tìm thấy host nào nằm ngoài CDN (edge servers).

---

#### **Bước 5: Kiểm tra thông tin hosting của từng subdomain**

- So sánh IP của từng subdomain với IP của tesla.com.
- Nếu trùng IP ⇒ khả năng cao dùng chung hosting/server backend.
- Có thể dùng lệnh: `nslookup`, `dig`, hoặc `host`.

---

#### **Bước 6: Phân tích thông tin WHOIS và ASN**

---

### 2.4 Kết luận

- Toàn bộ tên miền và subdomain của **Tesla** đều nằm sau **Akamai CDN**.
- Các IP thu được (`2.18.x.x`, `23.x.x.x`) đều thuộc hạ tầng Akamai, không phải server gốc của Tesla.
- Không phát hiện subdomain nào nằm ngoài CDN → **chưa xác định được IP thật của hệ thống Tesla bằng passive reconnaissance**.
- **Hướng phát triển:** Muốn tìm IP gốc cần dùng kỹ thuật nâng cao (historical DNS, Shodan, bypass CDN).

---
