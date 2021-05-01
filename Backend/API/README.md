# Arapgp Backend API

## 一、基本说明

本文件主要做以下三件事：

* 确定 `Arapgp Project` 中，`Front-end` 和 `Back-end` 之间的数据交换格式为 `json` ；
* 明确各 `API` 的 `Request Method / Path / Body` 以及对应的 `Response Body`；
* 明确各 `API` 的错误类型及后端对应的处理方式。

## 二、注意

* 本 `API` 中定义的 `status` 并非 `HTTP Respone` 中的 `status`（类型不同，含义不同），若要取到 `API` 中的 `status`，需要 `(HTTP Response Body).data.status`。
* 本 `API` 设计向 `RESTful-API` 的设计理念靠拢。
