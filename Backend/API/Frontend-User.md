
# Arapgp Backend API, Part.用户

该部分 `API` 针对数据库中 `User` 实体及其部分属性（包括但不限于 `User` 本身，`username`，`password`，`userid`）进行增删改查。

数据库中确有 `id` 字段，但该字段不适合传给前端，故将原本 `uid` 出现的地方改为其他具有等同效力的属性。

**注：`API` 中的字段仅作前后端交互使用，不同于数据库中字段**。

## 1. 注册

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

## 2. 登录

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
    | session | string | "asda2sd1354w3adsd2ad" |

  * Example

    * Normal

      ```json
      {
          "status": "OK",
          "lastLoginTime": "1970-01-01 12:34:59",
          "session": "asda2sd1354w3adsd2ad"
      }
      ```

    * Error

      * a. 用户名或密码错误

        ```json
        {
            "status": "Username or password wrong!"
        }
        ```

## 3. 登出

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

## 4. 根据用户名查询

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
    | userList | array[User(Object)] | [{ }, { }, { }] |

  * user(Object) Format

    | Key | Value-Type | Example |
    |-|-|-|
    | Username | string | "admin" |

  * Example

    ```json
    {
        "status": "OK",
        "userList": [
            {
                "Username": "admin"
            }
        ]
    }
    ```

  `userList` 长度默认最大为 10。
