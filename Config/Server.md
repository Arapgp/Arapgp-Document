# Arapgp Configuration -- Server

## 一、配置文件格式（暂定 / 样例）

```yaml
service:
    local:
        openpgp:
            storage:
              - type: "fs"
                item:
                # if userInfo uses fs to store, then
                # use "userInfo: string" in "item"
                    privateKeyRing: "i don't know"
                    publicKeyRing: "it doesn't matter"
                    file: "~/file"
            # if use db to store user info
              - type: "db"
                item:
                    host: "127.0.0.1"
                    port: 27017
                    username: "root"
                    password: "123456"

    client:
        ssl:
            port: 10080
            storage:
              - type: "fs"
                item:
                    crt: "~/.tls/secret.crt"
                    key: "~/.tls/secret.key"

    audit:
        ssh:
            port: 2222
            storage:
              - type: "fs"
                item:
                # audit log path includes all users' log file
                # or "log: '~/.log/audit.log'"
                    log: "~/.log/audit"

    config:
        ssh:
            port: 2224
            storage:
            - type: "fs"
                item:
                # config log path includes all users' config file
                # or "log: '~/.log/config.log'"
                    log: "~/.log/config"
```

## 二、有关服务

### 1. 对客户端服务

#### i. SSL/TLS

* 端口；
* 所用算法（如 `RSA-2048`，`ECDSA` 之类）；
* `.crt | .pem, .key` 文件的存取路径。

#### ii. OpenPGP

* 所用算法（如 `keygen` 的 `x25519`）；
* `privateKeyRing`；
* `publicKeyRing`。

如：

```yaml
# in db
openpgp:
    alg:
        keygen: "x25519"
        digest: "sha256"
```

### 2. 对配置&审计端服务

#### i. SSH

* 端口（两个或者一个）；
* `SSH` 共用算法；
* 二端各自的连接 / 使用日志存放路径。

如：

```yaml
# in db
ssh:
    alg:
        kex: "ecdh-sha2-nistp521"
        keygen: "ssh-rsa"
        encrypt: "aes256-ctr"
        digest: "hmac-sha2-512"
```

## 三、持久化数据

### 1. 利用文件系统

#### i. 公钥

```yaml
item:
    publicKeyRing: string
```

#### ii. 用户信息

用户信息可能有 “用户名”、“密码”。密码需处理后写入。
此外，`ssh / tls` 使用的 `keygen | kex | encrypt | mac | compress(if exists)` 算法，或许也需要存入文件中。

```yaml
item:
    userInfo: string
```

### 2. 利用数据库

如若利用数据库存储，那么需要：

```yaml
type: "db"
item:
    host: string
    port: int
    username: string
    password: string
```
