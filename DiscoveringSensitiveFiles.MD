# Discovering Sensitive Files Target Tesla.com
**Thực hiện:** Lê Thị Mỹ Tiên  
**Cập nhật lần cuối:** 30/07/2025  

## 1. Mục lục
- Mục tiêu
- Công cụ sử dụng
- Các bước thực hiện
- Kết luận

## 2. Nội dung

### 2.1 Mục tiêu
**Discovering Sensitive Files** là quá trình tìm và xác định các tệp nhạy cảm (cấu hình, backup, log, cơ sở dữ liệu, mã nguồn, khóa API…) bị lộ trên web hoặc hệ thống.  

Kỹ thuật này thường được thực hiện bằng:
- Google Dorking
- Quét thư mục/tệp bằng công cụ (dirb, gobuster)
- Kiểm tra repository công khai
- Shodan / Censys  

**Mục tiêu** là phát hiện những file có thể dẫn đến:
- Rò rỉ thông tin
- Chiếm quyền truy cập
- Tấn công leo thang  

**Biện pháp phòng ngừa**:
- Hạn chế file nhạy cảm trong thư mục public
- Chặn liệt kê thư mục
- Thiết lập quyền truy cập chặt chẽ
- Lọc dữ liệu khi đẩy mã nguồn  

**Các loại tệp nhạy cảm thường gặp**:
- **File cấu hình:** `.env`, `config.php`, `web.config`, `settings.py`
- **Backup & log:** `.bak`, `.old`, `.zip`, `.tar.gz`, `error.log`
- **Cơ sở dữ liệu:** `.sql`, `.db`, `.sqlite`
- **Thông tin xác thực:** file chứa mật khẩu, khóa API, chứng chỉ `.pem`, `.crt`
- **Mã nguồn:** `.git`, `.svn`

### 2.2 Công cụ sử dụng
- **Google Dorking** → Tìm kiếm file nhạy cảm qua cú pháp nâng cao trên Google.
- **gau (GetAllUrls)** → Thu thập tất cả URL liên quan đến domain từ các nguồn công cộng như Wayback Machine.
- **ffuf** → Dò tìm file/thư mục ẩn bằng wordlist, kiểm tra phản hồi 200/403.
- **GitHub Dorking** → Tìm thông tin nhạy cảm bị lộ trong các kho GitHub liên quan đến tên miền.

### 2.3 Các bước thực hiện

#### Bước 1: Dùng Google Dork để tìm file nhạy cảm
- site:tesla.com ext:env | ext:log | ext:sql | ext:bak | ext:old | ext:backup
- site:tesla.com intitle:"index of" "config" OR "backup"
**Kết quả:** Không có file nhạy cảm công khai qua Google Search vào thời điểm này.

#### Bước 2: Dùng gau để thu thập tất cả URL liên quan Tesla
- echo "tesla.com" | gau > urls.txt
- wc -l urls.txt
**Kết quả:**
- `0 urls.txt`: gau không thu thập được URL nào từ tesla.com.  
- Có thể Tesla đã chặn archive từ Wayback Machine, Common Crawl hoặc dùng `robots.txt`, `noindex`, `X-Robots-Tag: noarchive`.

#### Bước 3: Dò thư mục/file ẩn với ffuf
- Tạo wordlist:curl -O https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/raft-small-files.txt
- Dò:
ffuf -u https://tesla.com/FUZZ -w raft-small-files.txt -mc 200,403
ffuf -u https://tesla.com/FUZZ -w raft-small-files.txt -mc 200,403 -o tesla_fuzz_results.txt

**Kết quả:**
- Có hơn 100 endpoint `.php` được phát hiện: `admin.php`, `login.php`, `wp-login.php`, `xmlrpc.php`, `profile.php`, `sendmessage.php`, …
- Tất cả trả về **403 Forbidden** → endpoint tồn tại nhưng bị chặn truy cập (WAF, phân quyền).
- Không phát hiện file cấu hình nhạy cảm (`.env`, `.sql`) hay file backup (`.bak`, `.old`) → Tesla cấu hình bảo mật tốt.

#### Bước 4: Tìm file lộ trên GitHub
- Cài đặt GitHub Dorks
- Tạo GitHub Personal Access Token: echo "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" > tokens.txt
- Chạy tool:python github-dork.py -q tesla.com -t tokens.txt
Các tùy chọn:
- `-u` hoặc `--user`: Tìm trong một user cụ thể
- `-r` hoặc `--repo`: Tìm trong một repo cụ thể
- `-m` hoặc `--monit`: Kích hoạt chế độ theo dõi (monitor mode)

### 2.4 Kết luận
Qua quá trình kiểm tra:
- Không phát hiện tệp nhạy cảm bị lộ từ hệ thống Tesla qua Google Dorking, gau, ffuf và GitHub Dorking.
- Các endpoint tồn tại đều được bảo vệ bởi phân quyền hoặc tường lửa.
- Không có URL hay tệp cấu hình, backup nào bị rò rỉ.

**Kết luận:** Tesla đã triển khai biện pháp bảo mật tốt và kiểm soát chặt chẽ dữ liệu công khai.



