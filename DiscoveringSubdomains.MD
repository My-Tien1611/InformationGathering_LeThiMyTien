Tìm hiểu Discovering Subdomains Target Tesla.com
- Thực hiện: Lê Thị Mỹ Tiên
- Cập nhật lần cuối: 29/07/2025
1. Mục lục:
2. Nội dung:
- Công cụ sử dụng: Sublist3r
2.1 Mục tiêu:
Discovering Subdomains là bước thu thập thông tin (reconnaissance) để: tìm subdomains public của một domain (vd: shop.tesla.com, owners.tesla.com) và Phục vụ cho đánh giá bảo mật (pentest/red team) hoặc bug bounty.
2.2 Các bước thực hiện: 
Bước 1: Cài đặt: 
                git clone https://github.com/aboul3la/Sublist3r.git
                cd Sublist3r
                sudo pip install -r requirements.txt
                python sublist3r.py -d tesla.com -o tesla_subdomains.txt
Bước 2: 
