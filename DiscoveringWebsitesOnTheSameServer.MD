Tìm hiểu Discovering Websites On The Same Server:tesla.com
- Thực hiện: Lê Thị Mỹ Tiên
- Cập nhật lần cuối: 29/07/2025
1. Mục lục:
2. Nội dung:
2.1 Mục tiêu: 
Việc tìm các website khác cùng nằm trên một máy chủ thường nhằm các mục đích như mở rộng phạm vi kiểm thử và tìm lỗ hổng bảo mật (pentest), phân tích tối ưu hóa công cụ tìm kiếm để phát hiện mạng site vệ tinh hoặc hoạt động của đối thủ, hỗ trợ quản trị hệ thống và điều tra sự cố khi nhiều website dùng chung tài nguyên, cũng như phục vụ thu thập thông tin (OSINT) để có thêm dữ liệu liên quan đến tổ chức hay cá nhân.
2.2 Công cụ: 
2.3 Các bước thực hiện:
Giai đoạn 1: Initial Reconnaissance
Bước 1: Thu thập IP: nslookup tesla.com
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
- Lệnh nslookup tesla.com trả về nhiều địa chỉ IP khác nhau, cụ thể các dải 2.18.x.x và 23.x.x.x.
- Các dải IP này thuộc về Akamai Technologies (CDN), không phải hạ tầng trực tiếp của Tesla.
- Việc xuất hiện nhiều IP cho thấy Tesla đang sử dụng CDN kết hợp cơ chế load balancing để phân phối lưu lượng.
Bước 2: Tra cứu các domain cùng IP (Reverse IP Lookup):
Bước 2.1 Reverse lookup từng IP
nslookup 2.18.50.207
nslookup 23.40.100.207
nslookup 2.18.54.207
207.50.18.2.in-addr.arpa        name = a2-18-50-207.deploy.static.akamaitechnologies.com.
Authoritative answers can be found from:
207.100.40.23.in-addr.arpa      name = a23-40-100-207.deploy.static.akamaitechnologies.com.
Authoritative answers can be found from:
207.54.18.2.in-addr.arpa        name = a2-18-54-207.deploy.static.akamaitechnologies.com.
Bước 2.2 Online Reverse IP Tools:Truy cập viewdns.info/reverseip
- 2.18.50.207 và 23.40.100.207,...: Có 1 tên miền được lưu trữ trên máy chủ này: tesla.com
Kết quả cho thấy Tesla đang sử dụng Akamai CDN. Các IP này thuộc về Akamai Technologies, không phải server gốc của Tesla. 
Bước 3: Identify CDN/Protection:
RIFF�\
- Server: AkamaiGHost - Confirm Tesla dùng Akamai CDN
- Không detect Cloudflare - Loại trừ Cloudflare CDN
- Response headers chỉ từ edge servers

Bước 4: Sử dụng công cụ OSINT chuyên dụng
