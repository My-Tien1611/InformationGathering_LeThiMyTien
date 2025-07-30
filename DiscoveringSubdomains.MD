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
- Giới thiệu Sublist3r: 
Gói này chứa một công cụ bảo mật Python được thiết kế để liệt kê các tên miền phụ của trang web bằng OSINT. Công cụ này giúp các chuyên gia kiểm tra xâm nhập và chuyên gia săn lỗi thu thập và tập hợp các tên miền phụ cho tên miền mà họ nhắm mục tiêu trên mạng. Sublist3r liệt kê các tên miền phụ bằng nhiều công cụ tìm kiếm như Google, Yahoo, Bing, Baidu và Ask. Sublist3r cũng liệt kê các tên miền phụ bằng Netcraft, Virustotal, ThreatCrowd, DNSdumpster và ReverseDNS.
Subbrute được tích hợp với Sublist3r để tăng khả năng tìm kiếm nhiều tên miền phụ hơn bằng phương pháp bruteforce với danh sách từ được cải thiện
- Cài đặt và thử nghiệm:
                git clone https://github.com/aboul3la/Sublist3r.git
                cd Sublist3r
                sudo pip install -r requirements.txt
                python sublist3r.py -d tesla.com -o tesla_subdomains.txt
Cách 2: Subfinder
- Giới thiệu Subfinder:
Là một công cụ khám phá tên miền phụ, giúp tìm ra các tên miền phụ hợp lệ cho các trang web bằng cách sử dụng các nguồn trực tuyến thụ động. Công cụ này có kiến trúc mô-đun đơn giản và được tối ưu hóa về tốc độ. Subfinder được xây dựng chỉ để thực hiện một chức năng duy nhất - liệt kê tên miền phụ thụ động, và nó thực hiện điều đó rất tốt.
- Cài đặt và thử nghiệm:
                go install github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
- Liệt kê subdomains cơ bản: subfinder -d tesla.com
![image alt](https://github.com/My-Tien1611/InformationGathering_LeThiMyTien/blob/651804876166bd447a48805349b86c26aa418b14/Subdomains_Tesla.jpg)
Lệnh này sẽ quét tất cả các nguồn tích hợp sẵn để tìm subdomain của tesla.com và hiển thị ra màn hình.
- Quét sâu hơn (recursive) và lưu kết quả: 
                subfinder -d tesla.com -recursive -t 200 -v -o tesla_subdomains2.txt
Lệnh trên để tìm subdomain một cách đệ quy (recursive), chạy nhiều luồng (200 threads), ẩn banner, hiển thị chi tiết (verbose), và lưu kết quả
2.3 Nhận xét: 

