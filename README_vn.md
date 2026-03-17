# Môi trường Triển khai TCExam (TCExam Deployment Environments)

[English](README.md) | [🇻🇳 Tiếng Việt](README_vn.md)

Kho lưu trữ này cung cấp nhiều môi trường triển khai và hướng dẫn cho ứng dụng TCExam tùy thuộc vào hệ điều hành mục tiêu của bạn.

## Sao chép Kho lưu trữ (Cloning the Repository)

Kho lưu trữ này sử dụng Git submodules để lưu mã nguồn TCExam. Khi clone, vui lòng sử dụng cờ `--recursive`:

```sh
git clone --recursive https://github.com/phuong0111/tcexam-deploy.git
```

Nếu bạn đã clone kho lưu trữ mà không có cờ `--recursive`, bạn có thể khởi tạo submodule bằng cách chạy lệnh sau:

```sh
git submodule update --init --recursive
```

Vui lòng tham khảo tài liệu cụ thể bên dưới cho môi trường mục tiêu của bạn:

- [Hướng dẫn Triển khai Linux (Docker)](linux/README_vn.md)
- [Hướng dẫn Triển khai macOS (Docker)](macos/README_vn.md)
- [Hướng dẫn Triển khai Windows (Portable USB Ngoại tuyến)](windows/README_vn.md)
