# Discovering Subdomains Target Tesla.com

- **Thực hiện:** Lê Thị Mỹ Tiên  
- **Cập nhật lần cuối:** 29/07/2025  

## 1. Mục lục
1. [Mục tiêu](#21-mục-tiêu)
2. [Các cách thực hiện](#22-các-cách-thực-hiện)
   - [Cách 1: Sublist3r](#cách-1-sublist3r)
   - [Cách 2: Subfinder](#cách-2-subfinder)
3. [Nhận xét](#23-nhận-xét)

## 2. Nội dung

### Công cụ sử dụng: 
- **Sublist3r**
- **Subfinder**

### 2.1 Mục tiêu
Discovering Subdomains là bước thu thập thông tin (reconnaissance) để:
- Tìm các subdomain public của một domain (vd: shop.tesla.com, owners.tesla.com)
- Phục vụ cho đánh giá bảo mật (pentest/red team) hoặc bug bounty.

### 2.2 Các cách thực hiện

#### Cách 1: Sublist3r
**Giới thiệu Sublist3r**  
Sublist3r là công cụ bảo mật Python được thiết kế để liệt kê các tên miền phụ của trang web bằng OSINT.  
Công cụ này:
- Thu thập các tên miền phụ qua Google, Yahoo, Bing, Baidu, Ask
- Sử dụng Netcraft, Virustotal, ThreatCrowd, DNSdumpster, ReverseDNS
- Tích hợp Subbrute để brute force tìm thêm tên miền phụ

**Cài đặt và thử nghiệm**
```bash
git clone https://github.com/aboul3la/Sublist3r.git
cd Sublist3r
sudo pip install -r requirements.txt
python sublist3r.py -d tesla.com -o tesla_subdomains.txt
```

#### Cách 2: Subfinder
**Giới thiệu Subfinder**  
Subfinder là công cụ khám phá tên miền phụ thụ động, tối ưu về tốc độ, chỉ tập trung liệt kê tên miền phụ từ các nguồn online.

**Cài đặt và thử nghiệm**
```bash
go install github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

**Liệt kê subdomains cơ bản**
```bash
subfinder -d tesla.com
```

![image alt](https://github.com/My-Tien1611/InformationGathering_LeThiMyTien/blob/651804876166bd447a48805349b86c26aa418b14/Subdomains_Tesla.jpg)

**Quét sâu hơn và lưu kết quả**
```bash
subfinder -d tesla.com -recursive -t 200 -v -o tesla_subdomains2.txt
```

### 2.3 Nhận xét
Kết quả quét `tesla.com` với Sublist3r và Subfinder cho thấy:
- Rất nhiều subdomain thuộc nhiều hệ thống và dịch vụ: 
  - Trang chính: www.tesla.com, engage.tesla.com, accounts.tesla.com
  - API: api-account-master.tesla.com, ai-api.tesla.com, diner-api.tesla.com
  - Dev/staging/sandbox, quản trị nội bộ, email, thanh toán, học trực tuyến, năng lượng, GitHub nội bộ, cloud, VPN, ...
- Hạ tầng mạng của Tesla rất phức tạp, nhiều lớp dịch vụ, dễ trở thành mục tiêu kiểm thử bảo mật.

**Hướng pentest:**
1. Mở rộng bề mặt tấn công (thêm subdomain, endpoint ẩn)
2. Phân loại hệ thống (dev, staging, production)
3. Kiểm thử bảo mật web/API (XSS, SQLi, IDOR, SSRF)
4. Quét cổng, tìm cấu hình sai, file backup/secret
5. Báo cáo lỗ hổng qua bug bounty
