# HTB Nexus 靶机渗透测试报告

## 📋 项目信息

- **目标**：Hack The Box - Nexus (10.129.20.67)
- **难度**：Medium
- **报告日期**：2026.08.08
- **测试类型**：黑盒测试

## 🔗 攻击链

```
外部扫描 → 子域名枚举(git/billing) → Git历史泄露DB密码
→ 登录billing系统 → 文件上传绕过获取WebShell → 反弹Shell
→ .env文件泄露SSH密码 → SSH登录jones用户
→ Git模板功能执行build.py → SSH公钥写入宿主机
→ 容器逃逸 → root权限
```
  
## 🎯 核心漏洞

| # | 漏洞类型 | 分类 | 利用方式 |
|---|---------|------|---------|
| 1 | Git信息泄露 | OWASP A01:2021 / CWE-200 | 分析Git历史提交，提取.env中的数据库密码 |
| 2 | 文件上传绕过 | OWASP A03:2021 / CWE-434 | Burp Suite拦截修改文件扩展名，上传PHP Webshell |
| 3 | 硬编码凭证 | OWASP A05:2021 / CWE-798 | .env中明文密码被SSH服务复用 |
| 4 | 容器逃逸 | MITRE ATT&CK T1611 | Git模板build.py以root执行，构造恶意Git树对象写入authorized_keys |

## 🛠 使用工具

Nmap, ffuf, Firefox, Burp Suite, nc (Netcat), Git, SSH

## 📌 攻击链亮点

- **Git历史分析**：通过仓库提交历史中删除的记录，恢复出敏感配置文件（.env、docker-compose.yml）
- **文件上传绕过**：前端仅限制图片类型，后端无二次校验，Burp Suite拦截改扩展名即可上传PHP Webshell
- **密码复用链**：Git泄露的DB密码 → .env中的SSH密码 → 密码在多个服务间复用，形成横向移动通路
- **容器逃逸**：利用Git模板仓库的自动执行脚本（build.py），构造恶意Git树对象实现路径遍历，将攻击者SSH公钥写入宿主机/root/.ssh/authorized_keys

## 📁 文件结构

```
nexus/  
├── README.md ← 本文件
├── build.py ← 容器逃逸 PoC 脚本（Git模板功能利用）
├── Nexus渗透测试报告.pdf ← 完整报告
└── evidence/ ← 证据截图
```

## 📌 声明

所有测试均在 Hack The Box 合法靶场环境中进行，本报告仅用于个人学习与求职展示。
