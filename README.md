# (Bài tập tổng hợp) Giao Diện Dòng Lệnh Terminal Cơ Bản
## Phần 1 – CLI vs GUI và cấu trúc câu lệnh
### 1.	Phân tích cú pháp lệnh:
ls -Force C:\Windows\Logs
-	Command (Lệnh): ls
-	Options / Flags (Tham số/Cờ): -Force
-	Argument (Đối số): C:\Windows\Logs
### 2.	Vì sao phải dùng Terminal (PowerShell/SSH) để quản lý máy chủ Cloud?
Máy chủ Cloud đặt ở xa câm lặng, không có card đồ họa khủng hay màn hình giao diện (GUI) màu mè. Dùng CLI/Terminal chỉ tiêu tốn vài MB RAM để chạy các dòng chữ lệnh, nhường toàn bộ tài nguyên CPU và RAM tối đa cho việc chạy ứng dụng và phục vụ người dùng.
## Phần 2 – Điều hướng hệ thống file
### 1.	Relative Path để di chuyển
```PowerShell
cd .\quan-ly-sinh-vien\
```
### 2.	Absolute Path đầy đủ
```Plaintext
C:\Users\student\Desktop\quan-ly-sinh-vien\src\main.py
```
### 3.	Một lệnh PowerShell duy nhất
```PowerShell
ls -Force ..\data\
```
## Phần 3 – Thao tác file và thư mục
### 1.	Tạo đồng thời 2 thư mục con src và data trong quan-ly-sinh-vien
```PowerShell
mkdir quan-ly-sinh-vien\src, quan-ly-sinh-vien\data
```
### 2.	Tạo 3 file rỗng main.py, utils.py, README.md trong 1 dòng lệnh
```PowerShell
New-Item -ItemType File quan-ly-sinh-vien\src\main.py, quan-ly-sinh-vien\src\utils.py, quan-ly-sinh-vien\README.md
```
### 3.	Đổi tên và Sao lưu dự án
-	Đổi tên từ quan-ly-sv thành quan-ly-sinh-vien:
```PowerShell
mv quan-ly-sv quan-ly-sinh-vien
```
-	Sao lưu toàn bộ thư mục kèm con cái thành backup-quan-ly-sinh-vien:
```PowerShell
cp -Recurse quan-ly-sinh-vien backup-quan-ly-sinh-vien
```
## Phần 4 – Xử lý lỗi Terminal
### 1.	Phân tích Log lỗi số 2
-	**Chẩn đoán:** Đây là lỗi không tìm thấy đường dẫn hoặc tên thư mục không chính xác. Người dùng gõ sai scr thay vì src.
-	**Cách khắc phục:** Gõ cd sc sau đó nhấn phím Tab liên tục, PowerShell sẽ tự động điền thành src\. Nếu nó nhảy ra chữ khác hoặc không đổi nghĩa là thư mục đó không có thật.
### 2.	Phân tích Log lỗi số 3
-	**Chẩn đoán:** Đây là lỗi truy cập bị từ chối trên Windows. Nguyên nhân có thể do thiếu quyền truy cập, quyền thực thi hoặc chính sách bảo mật.
-	**Cách khắc phục:** Chạy lệnh cấp quyền tạm thời cho phép thực thi script trong phiên làm việc hiện tại:
```PowerShell
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process
```
Sau đó chạy lại lệnh .\setup.ps1 là mượt mà.
### 3.	Xử lý Log lỗi số 1
-	**Nguyên nhân:** Thư mục old-version còn chứa các file hoặc thư mục con. PowerShell yêu cầu xác nhận vì lệnh chưa chỉ định tham số xoá đệ quy.
-	**Đơn thuốc:**
```PowerShell
rm -Recurse -Force old-version
```
### 4.	Áp dụng Quy trình 3 bước đọc log lỗi cho Log lỗi số 4
|Bước | Câu trả lời|
|---|---|
|(a) Dòng chứa thông điệp lỗi trực tiếp nhất | FileNotFoundError: [Errno 2] No such file or directory: 'data/input.csv'|
|(b) Từ khóa lỗi (Error Keyword) | FileNotFoundError (Không tìm thấy file) |
|(c) Điều cần kiểm tra tiếp để sửa lỗi (vị trí đang đứng / đường dẫn trong code) | Vị trí đang chạy chương trình và đường dẫn tương đối ‘data/input.csv’ trong code|
