[toc]

# Arapgp Backend API

## 〇、基本说明

本文件主要做以下三件事：

* 确定 `Arapgp Project` 中，`Front-end` 和 `Back-end` 之间的数据交换格式为 `json` ；
* 明确各 `API` 的 `Request Method / Path / Body` 以及对应的 `Response Body`；
* 明确各 `API` 的错误类型及后端对应的处理方式。

### 1. 注意

* 本 `API` 中定义的 `status` 并非 `HTTP Respone` 中的 `status`（类型不同，含义不同），若要取到 `API` 中的 `status`，需要 `(HTTP Response Body).data.status`。
* 本 `API` 设计向 `RESTful-API` 的设计理念靠拢。

## 一、用户

该部分 `API` 针对数据库中 `User` 实体及其部分属性（包括但不限于 `User` 本身，`username`，`password`，`userid`）进行增删改查。

**注：`API` 中的字段仅作前后端交互使用，不同于数据库中字段**。

### 1. 注册

|Method|Path|
|-|-|
| POST | `/api/v1/signup` |

* Request Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | username | string | "test" |
    | password | string | "5e884898da280" |

  * Example

    ```json
    {
        "username": "test",
        "password": "5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8"
    }
    ```

* Response Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | status | string | "OK" |

  * Example

    * Normal:

      ```json
      {
          "status": "OK"
      }
      ```

    * Error

      * a. 用户名已存在

        ```json
        {
            "status": "Username already exists!"
        }
        ```

      * b. 用户名过长

        ```json
        {
            "status": "Username not legal!"
        }
        ```

### 2. 登录

|Method|Path|
|-|-|
| POST | `/api/v1/login` |

* Request Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | username | string | "skyleaworlder" |
    | password | string | "redlrowaelyks" |

  * Example

    ```json
    {
        "username": "skyleaworlder",
        "password": "redlrowaelyks"
    }
    ```

* Response Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | status | string | "OK" |
    | lastLoginTime | string | "1970-01-01 12:34:59" |
    | uid | int | 1 |

  * Example

    * Normal

      ```json
      {
          "status": "OK",
          "lastLoginTime": "1970-01-01 12:34:59",
          "uid": 1
      }
      ```

    * Error

      * a. 用户名或密码错误

        ```json
        {
            "status": "Username or password wrong!"
        }
        ```

### 3. 登出

|Method|Path|
|-|-|
| POST | `/api/v1/logout` |

* Response Body

  * Example

    * Normal

      | Key | Value-Type | Example |
      |-|-|-|
      | status | string | "OK" |

      ```json
      {
          "status": "OK"
      }
      ```

    * Error

      * a. 无权限

        ```json
        {
            "status": "Session does not exist!"
        }
        ```

### 4. 根据用户名查询

|Method|Path|
|-|-|
| GET | `/api/v1/user` |

* Param

  * Format

    |Key|Value-Example|
    |-|-|
    | query | admi |

  * Example

    query=admi

    **注：传入的是字符串，后端会按照给定的 “`username` 前缀” 到数据库中寻找匹配的用户**。

* Response Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | status | string | "OK" |
    | userList | array[user(Object)] | [{ }, { }, { }] |

  * user(Object) Format

    | Key | Value-Type | Example |
    |-|-|-|
    | uid | int | 1 |
    | username | string | "admin" |

  * Example

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

## 二、PGP

### 1. 查看公钥

| Method | Path |
|-|-|
| GET | `api/v1/pubKey` |

* Param

  * Format

    |Key|Value-Example|
    |-|-|
    | uid | 1 |

  * Example

    uid=1

* Response Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | status | string | "OK" |
    | pubKey | string | "a long text, much longer than you think" |

  * Example

    * Normal

      ```json
      {
          "status": "OK",
          "pubKey": "a long text, much longer than you think"
      }
      ```

    * Error

      * a. 公钥不存在

        ```json
        {
            "status": "PubKey does not exist!"
        }
        ```

      * b. 未登录

        ```json
        {
            "status": "Unauthenticated!"
        }
        ```

### 2. 上传公钥

| Method | Path |
|-|-|
| POST | `api/v1/pubKey` |

* Response Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | status | string | "OK" |

  * Example

    * Normal

      ```json
      {
          "status": "OK"
      }
      ```

    * Error

      * a. 未登录

        ```json
        {
            "status": "Unauthenticated!"
        }
        ```

### 3. 更改公钥

| Method | Path |
|-|-|
| PUT | `api/v1/pubKey` |

* Response Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | status | string | "OK" |

  * Example

    * Normal

      ```json
      {
          "status": "OK"
      }
      ```

    * Error

      * a. 未登录

        ```json
        {
            "status": "Unauthenticated!"
        }
        ```

### 4. 删除公钥

| Method | Path |
|-|-|
| DELETE | `api/v1/pubKey` |

* Response Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | status | string | "OK" |

  * Example

    * Normal

      ```json
      {
          "status": "OK"
      }
      ```

    * Error

      * a. 未登录

        ```json
        {
            "status": "Unauthenticated!"
        }
        ```
