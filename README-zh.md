# 如何用 MyBatis 连接到 TiDB

[![Java CI with Maven](https://github.com/tidb-samples/tidb-java-mybatis-quickstart/actions/workflows/maven.yml/badge.svg)](https://github.com/tidb-samples/tidb-java-mybatis-quickstart/actions/workflows/maven.yml)

[English](/README.md) | 中文

这是 PingCAP 为 MyBatis 编写的用于连接 TiDB 的示例项目

> TiDB 是一个兼容 MySQL 的数据库。[MyBatis](https://mybatis.org/mybatis-3/index.html) 是当前比较流行的开源 Java 应用持久层框架。

## 前置要求

- 推荐 **Java Development Kit** (JDK) **17** 及以上版本，你可以根据公司及个人需求，自行选择 [OpenJDK](https://openjdk.org/) 或 [Oracle JDK](https://www.oracle.com/hk/java/technologies/downloads/)。
- [Maven](https://maven.apache.org/install.html) **3.8** 及以上版本。
- [Git](https://git-scm.com/downloads)。
- TiDB 集群。如果你还没有 TiDB 集群，可以按照以下方式创建：
  - （推荐方式）参考[创建 TiDB Serverless 集群](https://docs.pingcap.com/tidbcloud/dev-guide-build-cluster-in-cloud)，创建你自己的 TiDB Cloud 集群。
  - 参考[部署本地测试 TiDB 集群](https://docs.pingcap.com/zh/tidb/stable/quick-start-with-tidb#部署本地测试集群)或[部署正式 TiDB 集群](https://docs.pingcap.com/zh/tidb/stable/production-deployment-using-tiup)，创建本地集群。

## 开始实践

### 1. 克隆示例代码仓库到本地

```shell
git clone https://github.com/tidb-samples/tidb-java-mybatis-quickstart.git
cd tidb-java-mybatis-quickstart
```

### 2. 配置连接信息

<details open>
<summary><b>(选项 1) TiDB Serverless</b></summary>

1. 在 TiDB Cloud 控制台中，打开 [Clusters](https://tidbcloud.com/console/clusters) 页面，选择你的 TiDB Serverless 集群，进入 **Overview** 页面，点击右上角的 **Connect** 按钮。
2. 确认窗口中的配置和你的运行环境一致。
    - **Endpoint Type** 为 **Public**
    - **Connect With** 为 **General**
    - Operating System 为你的运行环境
    > 如果你在 Windows Subsystem for Linux (WSL) 中运行，请切换为对应的 Linux 发行版。
3. 点击 **Generate password** 生成密码。
    > 如果你之前已经生成过密码，可以直接使用原密码，或点击 **Reset Password** 重新生成密码。
4. 运行以下命令，将 `env.sh.example` 复制并重命名为 `env.sh`：

    ```bash
    cp env.sh.example env.sh
    ```

5. 复制并粘贴对应连接字符串至 `env.sh` 中。需更改部分示例结果如下。

    ```shell
    export TIDB_HOST='{gateway-region}.aws.tidbcloud.com'
    export TIDB_PORT='4000'
    export TIDB_USER='{prefix}.root'
    export TIDB_PASSWORD='{password}'
    export TIDB_DB_NAME='test'
    export USE_SSL='true'
    ```

    注意替换 `{}` 中的占位符为 **Connect** 窗口中获得的值。

    TiDB Serverless 要求使用 secure connection，因此 `USE_SSL` 的值应为 `true`。

6. 保存文件。

</details>

<details>

<summary><b>(选项 2) TiDB Dedicated</b></summary>

1. 在 TiDB Cloud Web Console 中，选择你的 TiDB Dedicated 集群，进入 **Overview** 页面，点击右上角的 **Connect** 按钮。点击 **Allow Access from Anywhere**。
    > 更多配置细节，可参考 [TiDB Dedicated 标准连接教程](https://docs.pingcap.com/tidbcloud/connect-via-standard-connection).

2. 运行以下命令，将 `env.sh.example` 复制并重命名为 `env.sh`：

    ```bash
    cp env.sh.example env.sh
    ```

3. 复制并粘贴对应的连接字符串至 `env.sh` 中。需更改部分示例结果如下。

    ```shell
    export TIDB_HOST='{host}.clusters.tidb-cloud.com'
    export TIDB_PORT='4000'
    export TIDB_USER='{prefix}.root'
    export TIDB_PASSWORD='{password}'
    export TIDB_DB_NAME='test'
    export USE_SSL='false'
    ```

    注意替换 `{}` 中的占位符为 **Connect** 窗口中获得的值，并配置前面步骤中下载好的证书路径。

4. 保存文件。

</details>

<details>
<summary><b>(选项 3) 自建 TiDB</b></summary>

1. 运行以下命令，将 `env.sh.example` 复制并重命名为 `env.sh`：

    ```bash
    cp env.sh.example env.sh
    ```

2. 复制并粘贴对应的连接字符串至 `env.sh` 中。需更改部分示例结果如下。

    ```shell
    export TIDB_HOST='{tidb_server_host}'
    export TIDB_PORT='4000'
    export TIDB_USER='root'
    export TIDB_PASSWORD='{password}'
    export TIDB_DB_NAME='test'
    export USE_SSL='false'
    ```

    注意替换 `{}` 中的占位符为你的 TiDB 对应的值。如果你在本机运行 TiDB，默认 Host 地址为 `127.0.0.1`，密码为空。

3. 保存文件。

</details>

### 3. 运行示例代码

```shell
make
```

### 4. 期望输出

[期望的输出](/Expected-Output.txt)

## 注意事项

关于 MyBatis 的更多使用方法及细节，可以参考 [MyBatis 官方文档](http://www.mybatis.org/mybatis-3/)。

## 下一步

- 你可以继续阅读开发者文档，以获取更多关于 TiDB 的开发者知识。例如：[插入数据](https://docs.pingcap.com/zh/tidb/stable/dev-guide-insert-data)，[更新数据](https://docs.pingcap.com/zh/tidb/stable/dev-guide-update-data)，[删除数据](https://docs.pingcap.com/zh/tidb/stable/dev-guide-delete-data)，[单表读取](https://docs.pingcap.com/zh/tidb/stable/dev-guide-get-data-from-single-table)，[事务](https://docs.pingcap.com/zh/tidb/stable/dev-guide-transaction-overview)，[SQL 性能优化](https://docs.pingcap.com/zh/tidb/stable/dev-guide-optimize-sql-overview)等。
- 如果你更倾向于参与课程进行学习，我们也提供专业的 [TiDB 开发者课程](https://cn.pingcap.com/courses-catalog/back-end-developer/)支持，并在考试后提供相应的[资格认证](https://learn.pingcap.com/learner/certification-center)。
- 我们还有额外针对 Java 开发者的课程：[使用 Connector/J - TiDB v6](https://learn.pingcap.com/learner/course/840002/?utm_source=docs-cn-dev-guide) 及[在 TiDB 上开发应用的最佳实践 - TiDB v6](https://learn.pingcap.com/learner/course/780002/?utm_source=docs-cn-dev-guide) 可供选择。
