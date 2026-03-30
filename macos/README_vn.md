# Triển khai TCExam trên macOS

[English](README.md) | [🇻🇳 Tiếng Việt](README_vn.md)

## Cài đặt & Thiết lập

Thực hiện theo các bước sau để thiết lập môi trường triển khai TCExam trên macOS sử dụng Docker:

1. **Sao chép kho lưu trữ:**
```bash
git clone https://github.com/phuong0111/tcexam-deploy.git
```

2. **Điều hướng đến dự án và tạo thư mục mã nguồn:**
```bash
cd tcexam-deploy && mkdir source_code
```

3. **Vào thư mục mã nguồn:**
```bash
cd source_code
```

4. **Sao chép mã nguồn TCExam và khởi tạo cấu hình:**
```bash
git clone https://github.com/phuong0111/tcexam.git
cp -r tcexam/shared/config.example tcexam/shared/config
```

5. **Điều hướng đến thư mục cấu hình macOS:**
```bash
cd ../macos
```

6. **Xây dựng và khởi động các dịch vụ:**
```bash
docker-compose up --build -d
```
