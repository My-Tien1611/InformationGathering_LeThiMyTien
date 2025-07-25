# Gathering Information Using Whois Lookup Shopify.com

**Thực hiện:** Lê Thị Mỹ Tiên  
**Cập nhật:** 25/07/2025  

---

## Mục lục
- [1. Giới thiệu về Whois](#1-giới-thiệu-về-whois)  
- [2. Phương pháp nghiên cứu](#2-phương-pháp-nghiên-cứu)  
- [3. Thực hiện Whois Lookup Shopify.com](#3-thực-hiện-whois-lookup-shopifycom)  
  - [3.1 Thông tin cơ bản về domain](#31-thông-tin-cơ-bản-về-domain)  
  - [3.2 Thông tin DNS và kỹ thuật](#32-thông-tin-dns-và-kỹ-thuật)  
  - [3.3 Thông tin liên hệ](#33-thông-tin-liên-hệ)  
- [4. Phân tích kết quả](#4-phân-tích-kết-quả)  

---

## 1. Giới thiệu về Whois

**WHOIS** là giao thức truy vấn và phản hồi được sử dụng để truy vấn cơ sở dữ liệu lưu trữ thông tin người dùng đã đăng ký tài nguyên Internet, bao gồm tên miền và địa chỉ IP. Giao thức cung cấp thông tin cần thiết về:

- Quyền sở hữu tên miền  
- Thông tin liên hệ quản trị  
- Thông tin kỹ thuật  

Thông tin này rất có giá trị cho mục đích **quản lý** và **bảo mật tên miền**.

---

## 2. Phương pháp nghiên cứu

- **Công cụ sử dụng:**  
  - Online tool: [https://who.is/](https://who.is/)

---

## 3. Thực hiện Whois Lookup Shopify.com

### 3.1 Thông tin cơ bản về domain

- **Người đăng kí:** Công ty MarkMonitor  
- **Máy chủ Whois:** `whois.markmonitor.com`  
- **URL giới thiệu:** [http://www.markmonitor.com](http://www.markmonitor.com)  
- **Ngày quan trọng:**  
  - Ngày tạo: 11/03/2005  
  - Ngày hết hạn: 11/03/2027  
  - Đã cập nhật: 29/05/2025  
- **Trạng thái tên miền:**  
  - `clientDeleteProhibited`: [https://icann.org/epp#clientDeleteProhibited](https://icann.org/epp#clientDeleteProhibited)  
  - `clientTransferProhibited`: [https://icann.org/epp#clientTransferProhibited](https://icann.org/epp#clientTransferProhibited)  
  - `clientUpdateProhibited`: [https://icann.org/epp#clientUpdateProhibited](https://icann.org/epp#clientUpdateProhibited)  
  - `serverDeleteProhibited`: [https://icann.org/epp#serverDeleteProhibited](https://icann.org/epp#serverDeleteProhibited)  
  - `serverTransferProhibited`: [https://icann.org/epp#serverTransferProhibited](https://icann.org/epp#serverTransferProhibited)  

---

### 3.2 Thông tin DNS và kỹ thuật

#### Tên máy chủ & IP

| Tên máy chủ              | Địa chỉ IP        |
|--------------------------|-------------------|
| gold.foundationdns.com   | 172.64.40.2       |
| gold.foundationdns.net   | 172.64.40.32      |
| gold.foundationdns.org   | 108.162.198.62    |

#### Phân tích bản ghi DNS

![DNS Image](https://github.com/My-Tien1611/InformationGathering_LeThiMyTien/blob/db9168242cc857fa6fc297a8f43f0fefad6122f5/DNS.jpg)

**Các loại bản ghi DNS phổ biến gồm:**

- **SOA (Start of Authority):** Thông tin quản trị vùng  
- **NS (Nameserver):** Máy chủ tên có thẩm quyền  
- **A:** Ánh xạ tên miền đến địa chỉ IPv4  
- **AAAA:** Ánh xạ đến địa chỉ IPv6  
- **CNAME:** Tên chuẩn, alias đến domain khác  
- **MX (Mail Exchange):** Máy chủ thư  

- **Địa chỉ IP:** `23.227.38.33`  
- **Trạng thái DNSSEC:** `unsigned`  

---

### 3.3 Thông tin liên hệ

- **Người đăng kí:**  
  - Tổ chức: Công ty Shopify  
  - Địa chỉ: CA  
  - Email: Truy cập biểu mẫu tại  
    [https://domains.markmonitor.com/whois/shopify.com](https://domains.markmonitor.com/whois/shopify.com)

- **Liên hệ kỹ thuật:**  
  - Email: Truy cập biểu mẫu như trên  

---

## 4. Phân tích kết quả

Shopify.com thể hiện một cách tiếp cận **chuyên nghiệp** và **bảo mật cao** trong quản lý tên miền:

- **Gần 20 năm hoạt động**  
- Sử dụng **registrar cao cấp** (MarkMonitor)  
- Áp dụng đầy đủ các **biện pháp bảo vệ domain** (prohibited status)

**Tuy nhiên:**  
- **DNSSEC chưa được triển khai**, đây là một lỗ hổng bảo mật tiềm ẩn  
- Với vai trò là một nền tảng thương mại điện tử lớn, việc **bổ sung DNSSEC** sẽ giúp giảm rủi ro từ các cuộc tấn công dựa trên DNS

**Tổng kết:**  
Cấu hình domain của Shopify cho thấy một doanh nghiệp **trưởng thành**, có sự đầu tư nghiêm túc vào **bảo mật và hạ tầng**, nhưng vẫn còn **dư địa cải tiến** theo chuẩn **an ninh hiện đại**.

---
