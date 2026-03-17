# Hướng dẫn Triển khai USB Di động Ngoại tuyến cho TCExam

[English](README.md) | [🇻🇳 Tiếng Việt](README_vn.md)

Hướng dẫn này sẽ giúp bạn tạo một USB "cắm và chạy" để khởi chạy ứng dụng TCExam trên bất kỳ máy tính Windows nào mà không yêu cầu quyền quản trị viên, quyền truy cập internet hoặc cài đặt phần mềm.

## Điều kiện tiên quyết
*   Một Ổ đĩa Flash USB (khuyên dùng ít nhất 2GB không gian trống).
*   Một máy tính có kết nối internet (để tải xuống các tệp tin cần thiết ban đầu).
*   Mã nguồn TCExam hiện có của bạn mà bạn đã sao chép trước đó.

---

### Bước 1: Tải xuống XAMPP Portable

Chúng ta sẽ sử dụng XAMPP Portable vì nó gói gọn hoàn toàn Apache (máy chủ web), PHP và MySQL (máy chủ cơ sở dữ liệu) vào một thư mục duy nhất có thể chạy từ ổ USB.

1.  Điều hướng đến trang tải xuống chính thức của Apache Friends cho XAMPP Windows: [https://www.apachefriends.org/download.html](https://www.apachefriends.org/download.html)
2.  Tìm phiên bản có PHP 8.2 (Vì TCExam đã được kiểm tra và phù hợp với phiên bản 8.2).
3.  Nhấp vào "More Downloads".
4.  Điều hướng đến `XAMPP Windows` > Phiên bản bạn đã chọn (ví dụ: `8.2.12`).
5.  Tải xuống phiên bản portable **`.zip`** hoặc **`.7z`** (ví dụ: `xampp-portable-windows-x64-8.2.12-0-VS16.zip`). **KHÔNG tải xuống trình cài đặt `.exe`.**

### Bước 2: Giải nén vào Ổ USB

1.  Cắm thẻ USB vào máy tính của bạn.
2.  Giải nén tệp `xampp-portable...zip` đã tải xuống trực tiếp vào thư mục gốc của ổ USB của bạn (để bạn có một thư mục như `E:\xampp`).

### Bước 3: Chạy Kịch bản Thiết lập (Setup Script)

Để XAMPP portable có thể cấu hình chính xác các đường dẫn nội bộ của nó trên bất kỳ ký tự ổ đĩa nào được gán cho nó:
1.  Mở thư mục `xampp` trên ổ USB của bạn.
2.  Nhấp đúp chuột vào **`setup_xampp.bat`**.
3.  Một cửa sổ dòng lệnh sẽ xuất hiện ngắn gọn, cập nhật các tệp cấu hình. Nhấn enter khi nó nhắc bạn hoàn tất.

### Bước 4: Sao chép Mã nguồn TCExam

Bây giờ chúng ta cần đặt mã ứng dụng vào trong thư mục web của XAMPP.
1.  Điều hướng đến thư mục `htdocs` trong thư mục cài đặt XAMPP trên USB (`E:\xampp\htdocs`).
2.  Xóa bất kỳ tệp nào hiện có trong `htdocs` (như `index.php` hoặc thư mục `dashboard`) để giữ cho mọi thứ gọn gàng.
3.  Sao chép thư mục `tcexam` (thư mục nằm trong thư mục `source_code` của kho lưu trữ này) vào `htdocs`.
4.  Đường dẫn của bạn sẽ trông giống như sau: `E:\xampp\htdocs\tcexam`.

### Bước 5: Khởi động Máy chủ

1.  Quay lại thư mục gốc của thư mục `xampp` (`E:\xampp`).
2.  Nhấp đúp chuột vào **`xampp-control.exe`**.
3.  Bảng điều khiển sẽ xuất hiện. Nhấp vào **Start** bên cạnh **Apache** và **Start** bên cạnh **MySQL**.
    *(Nếu Windows Firewall nhắc bạn, hãy nhấp vào "Allow access").*

### Bước 6: Tạo Cơ sở Dữ liệu

Bây giờ chúng ta cần thiết lập cơ sở dữ liệu MySQL mà TCExam sẽ sử dụng.

1.  Mở trình duyệt web và đi đến: `http://localhost/phpmyadmin`
2.  Nhấp vào tab **"Databases"** ở trên cùng.
3.  Trong trường "Create database", nhập: `TCExam`
4.  Chọn `utf8mb4_unicode_ci` từ danh sách thả xuống Đối chiếu (Collation) bên cạnh nó.
5.  Nhấp vào **Create**.

### Bước 7: Nhập Cấu trúc Cơ sở Dữ liệu TCExam

TCExam đi kèm với các tệp SQL cần được nhập để thiết lập các bảng.

1.  Trong `phpMyAdmin`, đảm bảo cơ sở dữ liệu `TCExam` mới được chọn từ thanh bên trái.
2.  Nhấp vào tab **"Import"** ở trên cùng.
3.  Nhấp vào **"Choose File"**.
4.  Điều hướng đến ổ USB của bạn: `E:\xampp\htdocs\tcexam\install` và chọn tệp `mysql_db_structure.sql`.
5.  Cuộn xuống dưới cùng và nhấp vào **"Import"**.
6.  Sau khi thành công, hãy nhấp vào tab **"Import"** một lần nữa, nhấp vào **"Choose File"**, và lần này hãy chọn `db_data.sql` (cũng trong thư mục `install`).
7.  Nhấp vào **"Import"**.

### Bước 8: Cấu hình TCExam để Kết nối với Cơ sở Dữ liệu

Người dùng root MySQL mặc định của XAMPP **không có mật khẩu**. Chúng ta cần cho TCExam biết điều này.

1.  Trên ổ USB của bạn, điều hướng đến `E:\xampp\htdocs\tcexam\shared\config`.
2.  Mở tệp **`tce_db_config.php`** bằng trình soạn thảo văn bản (như Notepad).
3.  Tìm các dòng kết nối cơ sở dữ liệu và đảm bảo chúng trông giống hệt như sau:
    ```php
    define('K_DATABASE_TYPE', 'MYSQL');
    define('K_DATABASE_HOST', 'localhost');
    define('K_DATABASE_PORT', '3306');
    define('K_DATABASE_NAME', 'TCExam');
    define('K_DATABASE_USER_NAME', 'root');
    define('K_DATABASE_USER_PASSWORD', ''); // Để trống phần này cho XAMPP mặc định
    define('K_TABLE_PREFIX', 'tce_');
    ```
4.  Lưu và đóng tệp.

### Bước 9: Khởi chạy Ứng dụng!

Mọi thứ đã được thiết lập. Để chạy nó:
1.  Mở bất kỳ trình duyệt web nào.
2.  Điều hướng đến: `http://localhost/tcexam`
3.  Bạn sẽ nhìn thấy giao diện TCExam.
4.  Để truy cập bảng quản trị, hãy đi tới `http://localhost/tcexam/admin/code/` và đăng nhập bằng thông tin xác thực mặc định (Tên đăng nhập: `admin`, Mật khẩu: `1234`).

---

### Cách sử dụng trên Máy tính Windows Ngoại tuyến Mục tiêu:

1.  Ngắt kết nối an toàn ổ USB khỏi máy tính hiện tại của bạn.
2.  Cắm nó vào máy tính Windows ngoại tuyến mục tiêu.
3.  Mở ổ USB, mở thư mục `xampp`.
4.  Khởi chạy `xampp-control.exe` và khởi động **Apache** và **MySQL**.
5.  Mở trình duyệt web và đi đến `http://localhost/tcexam`.
6.  *Khi kết thúc:* Dừng các máy chủ trong bảng điều khiển trước khi rút USB.
