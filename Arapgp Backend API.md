[toc]

# Arapgp Backend API

## 用户

### 注册

- POST

- `/api/v1/signup`

- body

  ```json
  {
      "username":"test",
      "password":"5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8"
  }
  ```

- return

  ```json
  {
      "status": "OK"
  }
  ```

- error

  - 用户名已存在

    ```json
    {
        "status": "Username already exists!"
    }
    ```

  - 用户名过长

    ```json
    {
        "status": "Username not legal!"
    }
    ```

### 登录

- POST

- `/api/v1/login`

- body

  ```json
  {
      "name":"",
      "password":""
  }
  ```

- return

  ```json
  {
      "status": "OK",
      "lastLogin": "1970-01-01 12:34:59",
      "userid": 1
  }
  ```

- error

  - 用户名或密码错误

    ```json
    {
        "status": "Username or password wrong!"
    }
    ```

### 登出

- POST

- `/api/v1/login`

- return

  ```json
  {
      "status": "OK"
  }
  ```
  
- error

  - 无权限

    ```json
    {
        "status": "Session does not exist!"
    }
    ```

### 根据用户名查询

- GET

- `/api/v1/user`

- parameters

  - query=admin

- return

  ```json
  {
      "status": "OK",
      "userList": [
          {
              "uid":1,
              "username": "admin"
          }
      ]
  }
  ```

  `userList` 长度默认最大为 10。

## PGP

### 查看公钥

- GET

- `api/v1/pubKey`

- parameters

  - uid=1

- return

  ```json
  {
      "status": "OK",
      "pubKey": "a long text, much longer than you think"
  }
  ```

- error

  - 公钥不存在

    ```json
    {
        "status": "PubKey does not exist!"
    }
    ```

  - 未登录

    ```json
    {
        "status": "Unauthenticated!"
    }
    ```

### 上传公钥

- POST

- `api/v1/pubKey`

- return

  ```json
  {
      "status": "OK"
  }
  ```

- error

    - 未登录

      ```json
      {
          "status": "Unauthenticated!"
      }
      ```

### 更改公钥

- PUT

- `api/v1/pubKey`

- return

  ```json
  {
      "status": "OK"
  }
  ```

- error

    - 未登录

      ```json
      {
          "status": "Unauthenticated!"
      }
      ```

### 删除公钥

- DELETE

- `api/v1/pubKey`

- return

  ```json
  {
      "status": "OK"
  }
  ```

- error

    - 未登录

      ```json
      {
          "status": "Unauthenticated!"
      }
      ```