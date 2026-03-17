# TCExam Deployment Environments

[English](README.md) | [🇻🇳 Tiếng Việt](README_vn.md)

This repository provides multiple deployment environments and guides for the TCExam application depending on your target operating system.

## Cloning the Repository

This repository uses Git submodules to include the TCExam source code. When cloning, please use the `--recursive` flag:

```sh
git clone --recursive https://github.com/phuong0111/tcexam-deploy.git
```

If you have already cloned the repository without the `--recursive` flag, you can initialize the submodule by running:

```sh
git submodule update --init --recursive
```

Please refer to the specific documentation below for your target environment:

- [Linux Deployment Guide (Docker)](linux/README.md)
- [macOS Deployment Guide (Docker)](macos/README.md)
- [Windows Deployment Guide (Portable USB Offline)](windows/README.md)