# Arapgp Backend API, Part.File

## 1. 上传文件

为保证传输流量加密（不仅仅依靠 `SSL/TLS` 的流量加密），所有的加解密都在前端实现。因此，上传文件仍旧使用 `Content-Type: application/json`。

文件同样是不能重名的。因为都要放在一个（虚拟）文件夹下。

| Method | Path |
|-|-|
| POST | `api/v1/user/:username/file` |

* Request Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | name | string | "hahah.txt" |
    | content | string | "-----BEGIN PGP MESSAGE-----\n\nasdsadasda-----END PGP MESSAGE-----" |
    | pubKey | string | "a long text, much longer than you think" |

  * Example

    ```json
    {
        "name": "hahah.txt",
        "content": "-----BEGIN PGP MESSAGE-----\n\nasdsadasda-----END PGP MESSAGE-----",
        "pubKey": "a long text, much longer than you think"
    }
    ```

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

      * b. 意外错误

        ```json
        {
            "status": "Unexpected error!"
        }
        ```

      * c. 文件已存在

        ```json
        {
            "status": "File already exists!"
        }
        ```

      * d. 用户不存在

        ```json
        {
            "status": "User do not exist!"
        }
        ```

## 2. 获得文件

| Method | Path |
|-|-|
| GET | `api/v1/user/:username/file` |

* Param

  * Format

    |Key|Value-Example|
    |-|-|
    | name | "hahah.txt" |

  * Example

    name=hahah.txt

* Response Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | status | string | "OK" |
    | content | string | "-----BEGIN PGP MESSAGE-----\n\nasdsadasda-----END PGP MESSAGE-----" |

    * Normal

      ```json
      {
          "status": "OK",
          "content": "-----BEGIN PGP MESSAGE-----\n\nasdsadasda-----END PGP MESSAGE-----"
      }
      ```

    * Error

      * a. 未登录

        ```json
        {
            "status": "Unauthenticated!"
        }
        ```

      * b. 意外错误

        ```json
        {
            "status": "Unexpected error!"
        }
        ```

      * c. 文件不存在

        ```json
        {
            "status": "File do not exist!"
        }
        ```

      * d. 用户不存在

        ```json
        {
            "status": "User do not exist!"
        }
        ```

## 3. 修改文件

| Method | Path |
|-|-|
| PUT | `api/v1/user/:username/file` |

* Request Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | name | string | "hahah.txt" |
    | content | string | "-----BEGIN PGP MESSAGE-----\n\nasdsadasda-----END PGP MESSAGE-----" |

  * Example

    ```json
    {
        "name": "hahah.txt",
        "content": "-----BEGIN PGP MESSAGE-----\n\nasdsadasda-----END PGP MESSAGE-----"
    }
    ```

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

      * b. 意外错误

        ```json
        {
            "status": "Unexpected error!"
        }
        ```

      * c. 文件已存在

        ```json
        {
            "status": "File already exists!"
        }
        ```

      * d. 用户不存在

        ```json
        {
            "status": "User do not exist!"
        }
        ```

## 4. 删除文件

| Method | Path |
|-|-|
| DELETE | `api/v1/user/:username/file` |

* Request Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | name | string | "hahah.txt" |

  * Example

    ```json
    {
        "name": "hahah.txt"
    }
    ```

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

      * b. 意外错误

        ```json
        {
            "status": "Unexpected error!"
        }
        ```

      * c. 文件不存在

        ```json
        {
            "status": "File do not exist!"
        }
        ```

      * d. 用户不存在

        ```json
        {
            "status": "User do not exist!"
        }
        ```

## 5. 通过用户名获取文件信息

需要注意的是，本 `api` 并非通过文件名获取文件。而是通过用户名，获取所有用户下的所有文件。

| Method | Path |
|-|-|
| GET | `api/v1/user/:username/filesinfo` |

* Response Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | status | string | "OK" |
    | info | array |  |

  * Example

    * Normal

      ```json
      {
          "status": "OK",
          "info": [
            { "name": "hahah.txt", "author": "ljg", "createTime": "2021-05-27 09:49:13" }
          ]
      }
      ```

    * Error

      * a. 未登录

        ```json
        {
            "status": "Unauthenticated!"
        }
        ```

      * b. 意外错误

        ```json
        {
            "status": "Unexpected error!"
        }
        ```

      * c. 用户不存在

        ```json
        {
            "status": "User do not exist!"
        }
        ```
