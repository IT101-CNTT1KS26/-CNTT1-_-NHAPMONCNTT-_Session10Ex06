
# BÁO CÁO BÀI TẬP: PHÂN TÍCH BẢN CHẤT PLAIN TEXT VÀ MARKDOWN TRONG QUẢN LÝ MÃ NGUỒN (DỰ ÁN "GREENTECH")


---

## PHẦN 1: PHÂN TÍCH LỖI TRONG TƯ DUY LƯU TRỮ MÃ NGUỒN CỦA NAM

Trong bối cảnh phát triển phần mềm và quản lý phiên bản bằng Git/GitHub, việc lựa chọn định dạng tệp tin lưu trữ tài liệu kỹ thuật đóng vai trò quyết định đến hiệu suất làm việc nhóm. Việc Nam sử dụng Microsoft Word (`.docx` — định dạng Rich Text / Binary XML) thay vì Markdown (`.md` — Plain Text) đã dẫn đến hai sai lầm cốt lõi sau:

### 1. Sai lầm về cơ chế quản lý phiên bản và Git Diff (Xung đột toàn bộ tệp)

* **Bản chất của `.docx`:** Tệp Microsoft Word thực chất là một gói nén (ZIP) chứa rất nhiều tệp XML định nghĩa kiểu chữ, định dạng trang, cấu trúc đoạn văn và metadata. Đối với hệ thống Git, `.docx` được quản lý như một **tệp nhị phân (Binary File)**.
* **Hậu quả:** Khi Nam thay đổi dù chỉ một dấu phẩy, Git không thể đọc và so sánh chi tiết từng dòng nội dung (line-by-line diff). Thay vào đó, Git coi toàn bộ tệp đã bị thay đổi hoàn toàn. Khi các thành viên khác trong nhóm cùng đẩy code lên, hệ thống sẽ báo lỗi **Xung đột (Conflict) toàn bộ file** và các thành viên không thể xem trước nội dung trực tiếp trên giao diện web của GitHub mà bắt buộc phải tải tệp về máy mới đọc được.

### 2. Sai lầm về độ an toàn dữ liệu và tính chống hư hại (Data Corruption)

* **Bản chất độ bền của Plain Text so với Rich Text:**
* Định dạng Rich Text (`.docx`) có cấu trúc cấu thành cực kỳ chặt chẽ theo cây XML bên trong gói nén ZIP. Nếu quá trình truyền tải qua mạng gặp sự cố làm **mất hoặc lệch dù chỉ 1 byte dữ liệu**, toàn bộ cấu trúc gói nén sẽ bị phá vỡ. Khi mở file, Microsoft Word sẽ báo lỗi *"The file is corrupted and cannot be opened"* và Nam sẽ mất toàn bộ tài liệu.
* Ngược lại, **Markdown (`.md`) là Plain Text (Văn bản thô)**. Nó chỉ bao gồm các ký tự chữ cái tiêu chuẩn. Nếu gặp lỗi truyền mạng làm mất 1 byte, kết quả chỉ làm mất duy nhất 1 ký tự tại vị trí đó, phần còn lại của tài liệu vẫn mở đọc và chỉnh sửa hoàn toàn bình thường.


* **Ưu thế vượt trội của Markdown:** Vừa nhẹ, vừa chống hư hại dữ liệu tối đa, vừa tương thích tuyệt đối với các công cụ lập trình và hiển thị trực quan ngay trên trình duyệt web của GitHub.

---

## PHẦN 2: HOÀN THIỆN - TỆP MÃ NGUỒN MARKDOWN (`.md`) CHO DỰ ÁN "GREENTECH"

Để thay thế cho tệp Word cũ của Nam, dưới đây là phiên bản giới thiệu dự án "GreenTech" được chuẩn hóa bằng mã nguồn Markdown (`.md`) hoàn chỉnh, sẵn sàng đưa lên repository `[Tên Lớp]_[Môn Học]_Session08_Ex06`:

```markdown
#  GreenTech: Giải pháp Nông nghiệp Thông minh 4.0

Chào mừng đến với kho lưu trữ chính thức của dự án **GreenTech**. Dự án được xây dựng bởi đội ngũ sinh viên PTIT nhằm ứng dụng công nghệ IoT và AI để tối ưu hóa quy trình canh tác nông nghiệp, tiết kiệm tài nguyên nước và nâng cao năng suất cây trồng.

---

##  1. Giới thiệu Tổng quan
**GreenTech** là hệ thống giám sát và điều khiển tự động dành cho các mô hình trang trại công nghệ cao. Hệ thống giúp người nông dân theo dõi các thông số môi trường theo thời gian thực như:
- Độ ẩm đất và độ ẩm không khí.
- Nhiệt độ môi trường và cường độ ánh sáng.
- Trạng thái hoạt động của hệ thống máy bơm và van nước tự động.

---

##  2. Tính năng Nổi bật
- **Giám sát trực tuyến 24/7:** Cập nhật liên tục dữ liệu từ cảm biến thực địa lên Dashboard.
- **Tự động hóa thông minh:** Kích hoạt hệ thống tưới nước dựa trên ngưỡng độ ẩm cài đặt sẵn (Mô hình IPO).
- **Cảnh báo sớm:** Gửi thông báo trực tiếp qua ứng dụng khi môi trường vượt ngưỡng an toàn.

---

##  3. Bảng Công nghệ & Thiết bị Sử dụng

| Hạng mục | Tên công nghệ / Thiết bị | Mục đích sử dụng |
| :--- | :--- | :--- |
| **Vi điều khiển (SoC)** | ESP32 NodeMCU | Xử lý logic trung tâm và kết nối Wi-Fi |
| **Cảm biến** | DHT22 & Capacitive Soil Moisture | Đo đạc nhiệt độ, độ ẩm không khí và đất |
| **Ngôn ngữ lập trình** | Python & Markdown | Phát triển thuật toán điều khiển & viết tài liệu hệ thống |

---

##  4. Hướng dẫn Triển khai Mã nguồn

Để khởi chạy chương trình điều khiển cảm biến trên thiết bị biên, bạn sử dụng các lệnh Terminal sau:

```bash
# Clone repository về máy tính
git clone [https://github.com/ptit-greentech/greentech-iot.git](https://github.com/ptit-greentech/greentech-iot.git)

# Di chuyển vào thư mục dự án
cd greentech-iot

# Cài đặt thư viện phụ thuộc
pip install -r requirements.txt

# Chạy chương trình chính
python main.py

```

---

##  5. Lưu ý Phát triển (Git Workflow)

> **Khuyến nghị quan trọng:** Toàn bộ tài liệu kỹ thuật và mã nguồn của nhóm bắt buộc phải duy trì ở định dạng **Plain Text (.md)** để đảm bảo hệ thống Git theo dõi chính xác từng dòng thay đổi (Git Diff) và tránh tuyệt đối các lỗi xung đột tệp nhị phân khi làm việc nhóm!
