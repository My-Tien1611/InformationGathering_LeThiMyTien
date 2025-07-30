Tìm hiểu Discovering Sensitive Files Target Tesla.com
- Thực hiện: Lê Thị Mỹ Tiên
- Cập nhật lần cuối: 30/07/2025
1. Mục lục:
2. Nội dung
2.1 Mục tiêu:
2.2 Công cụ sử dụng:
2.3 Các bước thực hiện:
Bước 1: Thu thập subdomain từ bài lab trước subdomains.txt
Bước 2: Kiểm tra alive hosts:  cat tesla_subdomains.txt | httpx -silent -sc -title -o alive.txt
Bước 3: Directory & File brute-forcing: Tìm file nhạy cảm như .git, .env, .bak, .log, file backup bằng sử dụng công cụ ffuf hoặc dirsearch
Bước 4: Google Dorking (OSINT): Tìm file public nhạy cảm
Bước 5: Kiểm tra GitHub rò rỉ sử dụng tool GitDorker
