# TCExam macOS Deployment

[English](README.md) | [🇻🇳 Tiếng Việt](README_vn.md)

## Installation & Setup

Follow these steps to set up the TCExam deployment environment on macOS using Docker:

1. **Clone the repository:**
```bash
git clone https://github.com/phuong0111/tcexam-deploy.git
```

2. **Navigate to the project and create the source directory:**
```bash
cd tcexam-deploy && mkdir source_code
```

3. **Enter the source directory:**
```bash
cd source_code
```

4. **Clone the TCExam source code:**
```bash
git clone https://github.com/phuong0111/tcexam.git
```

5. **Navigate to the macOS configuration directory:**
```bash
cd ../macos
```

6. **Build and start the services:**
```bash
docker-compose up --build -d
```
