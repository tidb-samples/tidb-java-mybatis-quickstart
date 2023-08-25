# How to Connect to TiDB Using MyBatis

[![Java CI with Maven](https://github.com/tidb-samples/tidb-java-mybatis-quickstart/actions/workflows/maven.yml/badge.svg)](https://github.com/tidb-samples/tidb-java-mybatis-quickstart/actions/workflows/maven.yml)

English | [中文](/README-zh.md)

This is an example project by PingCAP for connecting to TiDB using the MyBatis.

> TiDB is a MySQL-compatible database. [MyBatis](https://mybatis.org/mybatis-3/index.html) is a currently popular open-source Java application persistence framework.

## Prerequisites

- Recommended **Java Development Kit** (JDK) version **17** or above. You can choose [OpenJDK](https://openjdk.org/) or [Oracle JDK](https://www.oracle.com/hk/java/technologies/downloads/) based on your company and personal needs.
- [Maven](https://maven.apache.org/install.html) version **3.8** or above.
- [Git](https://git-scm.com/downloads).
- TiDB cluster. If you don't have a TiDB cluster yet, you can create one using the following methods:
  - (Recommended) Refer to [Create TiDB Serverless Cluster](https://docs.pingcap.com/tidbcloud/dev-guide-build-cluster-in-cloud) to create your own TiDB Cloud cluster.
  - Refer to [Deploy a Local Testing TiDB Cluster](https://docs.pingcap.com/tidb/stable/quick-start-with-tidb#deploy-a-local-testing-cluster) or [Deploy a Production TiDB Cluster](https://docs.pingcap.com/tidb/stable/production-deployment-using-tiup) to create a local cluster.

## Getting Started

### 1. Clone the Example Code Repository to Your Local Machine

```shell
git clone https://github.com/tidb-samples/tidb-java-mybatis-quickstart.git
cd tidb-java-mybatis-quickstart
```

### 2. Configure Connection Information

<details open>
<summary><b>(Option 1) TiDB Serverless</b></summary>

1. In the TiDB Cloud console, open the [Clusters](https://tidbcloud.com/console/clusters) page, select your TiDB Serverless cluster, go to the **Overview** page, and click the **Connect** button in the upper right corner.
2. Ensure that the configuration in the window matches your runtime environment.
    - **Endpoint Type** is **Public**
    - **Connect With** is **General**
    - Operating System matches your runtime environment
    > If you are running in Windows Subsystem for Linux (WSL), switch to the corresponding Linux distribution.
3. Click **Generate password** to generate a password.
    > If you have generated a password before, you can use the original password or click **Reset Password** to generate a new one.
4. Run the following command to copy and rename `env.sh.example` to `env.sh`:

    ```shell
    cp env.sh.example env.sh
    ```

5. Copy and paste the corresponding connection string into `env.sh`. Change the example results as follows.

    ```shell
    export TIDB_HOST='{gateway-region}.aws.tidbcloud.com'
    export TIDB_PORT='4000'
    export TIDB_USER='{prefix}.root'
    export TIDB_PASSWORD='{password}'
    export TIDB_DB_NAME='test'
    export USE_SSL='true'
    ```

    Replace placeholders `{}` with values obtained from the **Connect** window.

    TiDB Serverless requires the use of a secure connection, so the value of `USE_SSL` should be set to `true`.

6. Save the file.

</details>

<details>

<summary><b>(Option 2) TiDB Dedicated</b></summary>

1. In the TiDB Cloud Web Console, select your TiDB Dedicated cluster, go to the **Overview** page, click the **Connect** button in the upper right corner. Click **Allow Access from Anywhere**.
    > For more configuration details, refer to [TiDB Dedicated Standard Connection Guide](https://docs.pingcap.com/tidbcloud/connect-via-standard-connection).

2. Run the following command to copy and rename `env.sh.example` to `env.sh`:

    ```shell
    cp env.sh.example env.sh
    ```

3. Copy and paste the corresponding connection string into `env.sh`. Change the example results as follows.

    ```shell
    export TIDB_HOST='{host}.clusters.tidb-cloud.com'
    export TIDB_PORT='4000'
    export TIDB_USER='{prefix}.root'
    export TIDB_PASSWORD='{password}'
    export TIDB_DB_NAME='test'
    export USE_SSL='false'
    ```

    Replace placeholders `{}` with values obtained from the **Connect** window, and configure the certificate path downloaded in previous steps.

4. Save the file.

</details>

<details>
<summary><b>(Option 3) Self-Hosted TiDB</b></summary>

1. Run the following command to copy and rename `env.sh.example` to `env.sh`:

    ```shell
    cp env.sh.example env.sh
    ```

2. Copy and paste the corresponding connection string into `env.sh`. Change the example results as follows.

    ```shell
    export TIDB_HOST='{tidb_server_host}'
    export TIDB_PORT='4000'
    export TIDB_USER='root'
    export TIDB_PASSWORD='{password}'
    export TIDB_DB_NAME='test'
    export USE_SSL='false'
    ```

    Replace placeholders `{}` with values corresponding to your TiDB setup. If you are running TiDB on your local machine, the default Host address is `127.0.0.1`, and the password is empty.

3. Save the file.

</details>

### 3. Run the Example Code

```shell
make
```

### 4. Expected Output

[Expected Output](/Expected-Output.txt)

## Notes

For more usage details and information about **MyBatis**, you can refer to the [official MyBatis documentation](http://www.mybatis.org/mybatis-3/).

## Next Steps

- You can continue reading the developer documentation to gain more knowledge about TiDB. For example: [Insert Data](https://docs.pingcap.com/tidb/stable/dev-guide-insert-data), [Update Data](https://docs.pingcap.com/tidb/stable/dev-guide-update-data), [Delete Data](https://docs.pingcap.com/tidb/stable/dev-guide-delete-data), [Read from a Single Table](https://docs.pingcap.com/tidb/stable/dev-guide-get-data-from-single-table), [Transactions](https://docs.pingcap.com/tidb/stable/dev-guide-transaction-overview), [SQL Performance Optimization](https://docs.pingcap.com/tidb/stable/dev-guide-optimize-sql-overview).
- If you prefer a structured learning approach, we provide professional course for Java developers: [Working with TiDB from Java](https://eng.edu.pingcap.com/catalog/info/id:212).
