# NK_static_download

NodeKeeper 的预编译二进制下载站。所有 tarball 走 **GitHub Releases**（单文件限 2GB）。

## 下载 URL 规则

```
https://github.com/linwoodpendleton/NK_static_download/releases/download/<component>/<tarball>
```

`<component>` 是 release tag。如：
- `nginx` — nginx normal/WAF × x86_64/aarch64
- `mysql` — MySQL 5.7/8.0/8.4 × x86_64/aarch64
- `mariadb` — MariaDB 10.6/10.11/11.4/11.8 × x86_64/aarch64
- `php` — PHP 5.2 → 8.5 × x86_64/aarch64（每个 PHP 版本带 ~88 个扩展）

## 文件命名规则

- `nginx-{normal|waf}-{x86_64|aarch64}.tar.gz`
- `{mysql|mariadb}-{version}-{x86_64|aarch64}.tar.gz`
- `php-{version}-{x86_64|aarch64}.tar.gz`

每个 `.tar.gz` 旁边都有对应 `.md5` 文件。

## 解压用法

```bash
# 下载 + 验证 + 解压
curl -fSL -o nginx.tar.gz https://.../nginx-normal-x86_64.tar.gz
curl -fSL -o nginx.tar.gz.md5 https://.../nginx-normal-x86_64.tar.gz.md5
md5sum -c nginx.tar.gz.md5
tar xzf nginx.tar.gz
```

## 已知系统依赖

WAF nginx 已经 bundle 了 libmodsecurity.so 到 `nginx/lib/`，但仍依赖系统的：
- libxml2 / libyajl / libstdc++ / libcurl / libxslt / libmaxminddb

Debian/Ubuntu: `apt install libxml2 libyajl2 libstdc++6 libcurl4 libxslt1.1 libmaxminddb0`

MySQL/MariaDB/PHP 各自有更长的系统依赖列表，参考 NK 仓库的 `install/install_{mysql,php}.sh` 里的 apt-get install 段落。

## 编译来源

所有 tarball 都用 NodeKeeper 仓库的 `install/install_{nginx,mysql,php}.sh` 编译，与 NK 在线安装产物一致。
