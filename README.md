# TransFlow - Lightweight File Transfer System

![C](https://img.shields.io/badge/C-Language-blue)
![Linux](https://img.shields.io/badge/Platform-Linux-orange)
![TCP](https://img.shields.io/badge/Protocol-TCP-green)
![SQLite](https://img.shields.io/badge/Database-SQLite3-lightgrey)

一个基于Linux TCP的C/S架构轻量级文件管理系统，支持多用户并发、大文件分块传输与安全认证。

## ✨ 核心特性

- 🔐 **用户认证系统** - MD5加密密码存储，替代明文存储风险
- 📁 **大文件分块传输** - 支持任意大小文件稳定传输，成功率100%
- 🔄 **多线程并发** - 支持≥5客户端同时访问，线程安全
- 📊 **实时操作日志** - 完整记录用户操作，便于审计追溯
- 🎯 **自定义通信协议** - 解决TCP粘包问题，传输稳定可靠

## 🏗 系统架构

### 通信协议设计
为解决TCP粘包问题，设计了自定义应用层协议：

```c
struct net_data {
    int type;      // 操作类型 (上传/下载/认证等)
    int offset;    // 分块标记 (0=开始, 1=中间块, 2=结束)
    int data_len;  // 数据长度
    char data[0];  // 柔性数组指向实际数据
};
