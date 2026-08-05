# Penetration Testing Reports

个人渗透测试实战报告集合，所有测试均在合法靶场环境中进行。

## 📋 报告列表

### HTB Cap 靶机渗透测试报告
- 目标：Hack The Box - Cap (10.129.17.78)
- 难度：Easy
- 攻击链：外部扫描 → IDOR越权 → PCAP分析提取FTP凭证 → SSH登录 → Python cap_setuid提权
- 报告文件：[Cap渗透测试报告.pdf]

### 漏洞清单
| 漏洞类型 | CWE/分类 | 利用过程 |
|---------|---------|---------|
| IDOR | CWE-639 | 枚举/data目录ID，越权下载PCAP文件 |
| 敏感信息泄露 | OWASP A01:2021 | PCAP中包含FTP明文凭证 |
| 特权提升 | MITRE ATT&CK T1548.001 | Python cap_setuid能力滥用 |

## 🛠 使用工具
Nmap, Firefox, Wireshark, getcap, ffuf

## 📌 声明
本报告仅用于个人学习与求职展示，所有测试均在 Hack The Box 合法靶场中进行，未对任何未经授权的系统发起攻击。
