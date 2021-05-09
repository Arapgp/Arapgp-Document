# Arapgp Backend API, Part.File

## 1. 上传文件

为保证传输流量加密（不仅仅依靠 `SSL/TLS` 的流量加密），所有的加解密都在前端实现。因此，上传文件仍旧使用 `Content-Type: application/json`。

文件同样是不能重名的。因为都要放在一个（虚拟）文件夹下。

| Method | Path |
|-|-|
| POST | `api/v1/file` |

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

## 2. 获得文件

| Method | Path |
|-|-|
| GET | `api/v1/pubKey` |

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

## 3. 修改文件

| Method | Path |
|-|-|
| PUT | `api/v1/file` |

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

## 4. 删除文件

| Method | Path |
|-|-|
| DELETE | `api/v1/file` |

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
