# Xboard

## 安装指南

本指南将指导您完成 Xboard 的安装和配置。

### 步骤 1: 克隆仓库

首先，克隆本项目到您的本地机器：

### 步骤 2: 配置 Docker

1. 打开 `docker-compose.yaml` 文件。
2. 将文件中的 `[U_PASSWD]` 替换为您希望设置的密码。

### 步骤 3: 配置数据库

运行以下命令来配置数据库：

```bash
# 数据库地址设置为 mariadb，名称设为 xboard，用户名 xboard，密码使用您在前一步设置的密码
# Redis 地址设置为 redis，端口使用默认值，密码同样使用默认值
# 重要：请记住返回输出的内容！
docker compose run -it --rm xboard php artisan xboard:install
```

### 步骤 4: 启动服务

使用以下命令来启动 Xboard 服务：

```bash
docker compose up -d
```

### 步骤 5: 访问 Xboard 面板

在浏览器中访问 `127.0.0.1:7001`，您将看到 Xboard 面板。

---

请确保在安装和配置过程中遵循以上步骤，以确保 Xboard 的正确安装和运行。

* 贴一个Caddy配置
```Caddyfile
[U_DOMAIN] {
    reverse_proxy http://127.0.0.1:7001 {
        header_up Host {host}
        header_up X-Real-IP {remote}
        header_up X-Forwarded-For {remote}
    }
    encode zstd gzip
}
```
