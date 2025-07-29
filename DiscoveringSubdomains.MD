Tìm hiểu Discovering Subdomains Target Tesla.com
- Thực hiện: Lê Thị Mỹ Tiên
- Cập nhật lần cuối: 29/07/2025
1. Mục lục:
2. Nội dung:
- Công cụ sử dụng: Sublist3r
2.1 Mục tiêu:
Discovering Subdomains là bước thu thập thông tin (reconnaissance) để: tìm subdomains public của một domain (vd: shop.tesla.com, owners.tesla.com) và Phục vụ cho đánh giá bảo mật (pentest/red team) hoặc bug bounty.
2.2 Các cách thực hiện: 
Cách 1: Sublist3r
                git clone https://github.com/aboul3la/Sublist3r.git
                cd Sublist3r
                sudo pip install -r requirements.txt
                python sublist3r.py -d tesla.com -o tesla_subdomains.txt
Cách 2: Subfinder
                go install github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
- Liệt kê subdomains cơ bản: subfinder -d tesla.com
![image alt](https://github.com/My-Tien1611/InformationGathering_LeThiMyTien/blob/651804876166bd447a48805349b86c26aa418b14/Subdomains_Tesla.jpg)
Lệnh này sẽ quét tất cả các nguồn tích hợp sẵn để tìm subdomain của tesla.com và hiển thị ra màn hình.
- Quét sâu hơn (recursive) và lưu kết quả: 
                subfinder -d tesla.com -recursive -silent -t 200 -v -o tesla_subdomains.txt
Để tìm subdomain một cách đệ quy (recursive), chạy nhiều luồng (200 threads), ẩn banner, hiển thị chi tiết (verbose), và lưu kết quả
- Sử dụng bruteforce để mở rộng kết quả: 
