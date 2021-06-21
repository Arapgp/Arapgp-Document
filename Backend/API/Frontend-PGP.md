# Arapgp Backend API, Part.PGP

## 1. 查看公钥

| Method | Path |
|-|-|
| GET | `api/v1/pubKey` |

* Param

  * Format

    |Key|Value-Example|
    |-|-|
    | username | "ljg" |

  * Example

    username="ljg"

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

## 2. 上传公钥

| Method | Path |
|-|-|
| POST | `api/v1/pubKey` |

* Request Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | pubKey | string | "a long text, much longer than you think" |
    | username | string | "ljg" |

  * Example

    ```json
    {
        "pubKey": "a long text, much longer than you think",
        "username": "ljg"
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

## 3. 更改公钥

| Method | Path |
|-|-|
| PUT | `api/v1/pubKey` |

* Request Body

  * Format

    | Key | Value-Type | Example |
    |-|-|-|
    | pubKey | string | "a long text, much longer than you think" |

  * Example

    ```json
    {
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

## 4. 删除公钥

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
