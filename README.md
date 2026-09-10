# Penetration Testing Reports

个人渗透测试实战报告集合，所有测试均在合法靶场环境中进行。

## 📋 项目列表

### 1. HTB Cap 靶机渗透测试报告
- **目标**：Hack The Box - Cap (10.129.17.78)
- **难度**：Easy
- **核心漏洞**：IDOR (CWE-639) + cap_setuid提权
- **攻击链**：外部扫描 → IDOR越权 → PCAP分析提取FTP凭证 → SSH登录 → Python cap_setuid提权
- **详情**：[cap/README.md](./cap/README.md)

### 2. HTB Nexus 靶机渗透测试报告
- **目标**：Hack The Box - Nexus (10.129.20.67)
- **难度**：Medium
- **核心漏洞**：Git信息泄露 + 文件上传绕过 + 硬编码凭证 + 容器逃逸
- **攻击链**：子域名枚举 → Git历史泄露密码 → 文件上传绕过获取WebShell → .env泄露SSH密码 → Git模板build.py容器逃逸 → root
- **详情**：[nexus/README.md](./nexus/README.md)

## 🛠 常用工具

Nmap, ffuf, Firefox, Burp Suite, Wireshark, LinPEAS/getcap, nc (Netcat), Git, Metasploit, SSH

## 📌 声明

所有测试均在合法授权的靶场环境中进行，本报告仅用于个人学习与求职展示。
