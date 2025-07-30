# Tìm hiểu Discovering Google Hacking Target Tesla.com
- **Thực hiện:** Lê Thị Mỹ Tiên  
- **Cập nhật lần cuối:** 30/07/2025

---

## 1. Mục lục
- [Mục tiêu](#21-mục-tiêu)
- [Các bước thực hiện](#22-các-bước-thực-hiện)
- [Kết luận](#23-kết-luận)

---

## 2. Nội dung

### 2.1 Mục tiêu:
Mục tiêu của kỹ thuật **Google Hacking (Google Dorking)** là thu thập thông tin công khai từ hệ thống mục tiêu bằng cách sử dụng các cú pháp tìm kiếm nâng cao trên Google.  
Kỹ thuật này nhằm phát hiện các tệp tin nhạy cảm như:
- File cấu hình, backup
- Log hệ thống
- Cơ sở dữ liệu
- API key
- Các trang quản trị hoặc tài liệu nội bộ bị lộ công khai trên Internet

Đây là bước thu thập thông tin thụ động giúp đánh giá sơ bộ mức độ rò rỉ dữ liệu, hỗ trợ quá trình kiểm thử bảo mật một cách hiệu quả mà không cần tương tác trực tiếp với hệ thống.

---

### 2.2 Các bước thực hiện:

#### 🔍 Tìm file cấu hình, backup, mã nguồn  
**Dork:**  
`site:tesla.com ext:env | ext:log | ext:sql | ext:bak | ext:old | ext:ini`  
**Kết quả:**  
- Không tìm thấy kết quả nào phù hợp với truy vấn trên Google.

---

#### 🔍 Tìm trang quản trị  
**Dork:**  
`site:tesla.com inurl:admin | inurl:login | intitle:"admin login"`  
**Kết quả:**  
- `/user/login`: là trang đăng nhập người dùng, không có gì nhạy cảm.  
- `feedback.tesla.com/login`: chứa nội dung `{{LOGIN.BROWSER_NOT_SUPPORT}}`, cho thấy có thể là ứng dụng nội bộ đang render sai.  
- Không tìm thấy trang quản trị rõ ràng, nhưng xuất hiện vài endpoint có thể liên quan tới hệ thống nội bộ hoặc cũ.

---

#### 🔍 Tìm tài liệu chứa thông tin nhạy cảm  
**Dork:**  
`site:tesla.com filetype:pdf | filetype:xls | filetype:doc "confidential" | "internal use only"`  
**Kết quả:**  
- Một số tài liệu PDF của Tesla chứa cụm từ “confidential” hoặc “internal use only”, ví dụ: *Annual Meeting Drawing Terms*, *Training Requirements*.  
- Dù chưa chắc là tài liệu rò rỉ, nhưng có thể dùng để phân tích các thông tin nội bộ công khai ngoài ý muốn. Đây là nguồn thông tin OSINT hữu ích.

---

#### 🔍 Tìm file chứa API key, token...  
**Dork:**  
`site:tesla.com "api_key" | "token" | "secret_key"`  
**Kết quả:**  
- Chủ yếu là tài liệu hướng dẫn của API Tesla Fleet.  
- Các kết quả mô tả về cách dùng Bearer token, Partner Tokens, OAuth token.  
- Không lộ API key thật, nhưng từ đây có thể hiểu cách xác thực của hệ thống.  
- Đây là thông tin nền tảng tốt cho việc fuzz hoặc kiểm tra bảo mật API sau này.

---

#### 🔍 Tìm thư mục lộ chỉ mục  
**Dork:**  
`site:tesla.com intitle:"index of"`  
**Kết quả:**  
- Không tìm thấy Directory Listing mở (index of).  
- Chỉ hiện các trang có chứa từ "Index" trong nội dung PDF hoặc tiêu đề.  
- Tesla đã vô hiệu hóa directory listing, điều này là tốt về mặt bảo mật.  
- Dork này không mang lại thông tin hữu ích trong trường hợp này.

---

#### 🔍 Tìm các lỗi hoặc log hệ thống  
**Dork:**  
`site:tesla.com "Fatal error" | "Warning" | "Notice"`  
**Kết quả:**  
- Chủ yếu là các cảnh báo an toàn cho người dùng trên dòng xe Tesla.  
- Không có lỗi hệ thống, log nội bộ hoặc thông báo lỗi từ web backend.  
- Dork không thành công trong việc tìm log lộ ra ngoài.  
- Tuy nhiên xác nhận rằng các thông báo kỹ thuật frontend không gây lộ thông tin.

---

### 2.3 Kết luận:
Quá trình **Google Dorking** đối với Tesla.com cho thấy rằng hầu hết các thông tin nhạy cảm như tệp cấu hình, file backup hay lỗi hệ thống **đã được kiểm soát tốt** và **không bị lộ công khai**.  

Tuy nhiên, vẫn thu được một số **tài liệu nội bộ** định dạng PDF có chứa cụm từ như *"confidential"* hoặc *"internal use only"*, cùng với một vài **endpoint đăng nhập** và **tài liệu API mô tả cách sử dụng token**.  

Mặc dù không phát hiện **lỗ hổng nghiêm trọng**, kết quả cho thấy Tesla **quản lý khá chặt chẽ việc index nội dung nhạy cảm trên Google**, nhưng **vẫn có thể cải thiện thêm** về kiểm soát metadata tài liệu và hiển thị giao diện của một số hệ thống nội bộ.

---
