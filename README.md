
<!-- identity-block -->
<div align="center">

# zerobus-sdk

<sub>Databricks's Zerobus Ingest SDKs.</sub>

</div>

## At a glance

| Field | Detail |
| --- | --- |
| Repository | zerobus-sdk |
| Primary language | Rust |
| Topics | cpp, data-ingestion, databricks, go, java, python, rust, sdk, typescript |
| License | Apache-2.0 |
| Branch | main |
| Maintainer | [@devarent](https://github.com/devarent) |

## Overview

zerobus-sdk is a hands-on repository focused on: Databricks's Zerobus Ingest SDKs.. Primary language: Rust. Topics: cpp, data-ingestion, databricks, go, java, python, rust, sdk, typescript. The README below documents the project; use the table above for a quick overview.

### Global references

<div align="center">

🇮🇸 Iceland &middot; 🇳🇿 New Zealand &middot; 🇨🇭 Switzerland &middot; 🇸🇮 Slovenia &middot; 🇮🇪 Ireland &middot; 🇦🇹 Austria &middot; 🇵🇹 Portugal &middot; 🇸🇬 Singapore &middot; 🇫🇮 Finland

</div>

---

<!-- dbx-style-kit -->
<div align="center">

<img src="https://img.shields.io/badge/zerobus-sdk-1f6feb?style=for-the-badge" alt="zerobus-sdk" />
<img src="https://img.shields.io/badge/LANG%20Rust-3178c6?style=for-the-badge" alt="LANG Rust" />
<img src="https://img.shields.io/badge/STARS%201-eab308?style=for-the-badge" alt="STARS 1" />
<img src="https://img.shields.io/badge/LICENSE%20Apache-2.0-22c55e?style=for-the-badge" alt="LICENSE Apache-2.0" />

<br>

<img src="https://img.shields.io/badge/OPEN%20SOURCE-yes-22c55e?style=for-the-badge&logo=github&logoColor=white" alt="OPEN SOURCE" />
<img src="https://img.shields.io/badge/BUILT%20IN%20PUBLIC-true-6366f1?style=for-the-badge&logo=opensourceinitiative&logoColor=white" alt="BUILT IN PUBLIC" />
<img src="https://img.shields.io/badge/HANDS%20ON%20LABS-52-0ea5e9?style=for-the-badge&logo=docker&logoColor=white" alt="HANDS ON LABS" />
<img src="https://img.shields.io/badge/DOCUMENTED-yes-14b8a6?style=for-the-badge&logo=markdown&logoColor=white" alt="DOCUMENTED" />

<br>

<b>Databricks's Zerobus Ingest SDKs.</b>

</div>

---
# Zerobus SDKs

Monorepo for Databricks Zerobus Ingest SDKs.

## Disclaimer

[GA](https://docs.databricks.com/release-notes/release-types.html): This SDK is generally available and supported for production use cases. Minor and patch version updates will not contain breaking changes. Major version updates may include breaking changes.

We are keen to hear feedback from you. Please [file issues](https://github.com/databricks/zerobus-sdk/issues), and we will address them.

## What is Zerobus?

Zerobus is a high-throughput streaming service for direct data ingestion into Databricks Delta tables, optimized for real-time data pipelines and high-volume workloads.

## SDKs

| Language   | Directory                    | Package                                                                                                        |
| ---------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------- |
| Rust       | [`rust/`](rust/)             | [`databricks-zerobus-ingest-sdk`](https://crates.io/crates/databricks-zerobus-ingest-sdk)                      |
| Python     | [`python/`](python/)         | [`databricks-zerobus-ingest-sdk`](https://pypi.org/project/databricks-zerobus-ingest-sdk/)                     |
| Go         | [`go/`](go/)                 | [`github.com/databricks/zerobus-sdk/go`](https://pkg.go.dev/github.com/databricks/zerobus-sdk/go)              |
| TypeScript | [`typescript/`](typescript/) | [`@databricks/zerobus-ingest-sdk`](https://www.npmjs.com/package/@databricks/zerobus-ingest-sdk)               |
| Java       | [`java/`](java/)             | [`com.databricks:zerobus-ingest-sdk`](https://central.sonatype.com/artifact/com.databricks/zerobus-ingest-sdk) |
| C++        | [`cpp/`](cpp/)               | Source / CMake (`zerobus::zerobus`)                                                                            |
| C#         | [`dotnet/`](dotnet/)         | [`Databricks.Zerobus.Ingest.Sdk`](https://www.nuget.org/packages/Databricks.Zerobus.Ingest.Sdk)                |

## Platform Support

We try to provide prebuilt native binaries for the following platforms:

| Platform | Architecture            |
| -------- | ----------------------- |
| Linux    | x86_64                  |
| Linux    | aarch64                 |
| Windows  | x86_64                  |
| macOS    | x86_64                  |
| macOS    | aarch64 (Apple Silicon) |

> **Note:** We do not currently have macOS CI runners, so macOS binaries are built locally and may not be available for every SDK or release. If your platform is not supported or you encounter compatibility issues, you can [build from source](CONTRIBUTING.md) or [file an issue](https://github.com/databricks/zerobus-sdk/issues).

## Prerequisites

Before using any SDK, you need the following:

### 1. Connection URLs and Workspace ID

Every SDK takes two URLs: the Databricks workspace URL, used for Unity Catalog and OAuth,
and the Zerobus server endpoint, used for ingestion. Their format depends on the cloud
that hosts your workspace:

| Cloud | Databricks workspace URL | Zerobus server endpoint |
| ----- | ------------------------ | ----------------------- |
| AWS | `https://<databricks-instance>.cloud.databricks.com` | `https://<workspace-id>.zerobus.<region>.cloud.databricks.com` |
| Azure | `https://<databricks-instance>.azuredatabricks.net` | `https://<workspace-id>.zerobus.<region>.azuredatabricks.net` |
| GCP | `https://<databricks-instance>.gcp.databricks.com` | `https://<workspace-id>.zerobus.<region>.gcp.databricks.com` |

After logging into your workspace, look at the browser URL, for example
`https://<databricks-instance>.cloud.databricks.com/?o=<workspace-id>`:

- Workspace URL: everything before `/?o=`. Use it exactly as shown.
- Workspace ID: the number after `o=`. If the browser URL has no `o=` parameter, copy
  the ID from the account console or the workspace details page.
- Region: the cloud region the workspace is deployed in, such as `us-west-2` on AWS,
  `eastus2` on Azure, or `us-east1` on GCP.

The Zerobus endpoint is built from the workspace ID and region, not from the workspace
host. On GCP, for example, the workspace URL `https://1234567890123456.0.gcp.databricks.com`
pairs with the endpoint `https://1234567890123456.zerobus.us-east1.gcp.databricks.com`.

Pass both values as complete URLs, including `https://`, for consistent behavior across
SDKs.

### 2. Create a Delta Table

Create a table using Databricks SQL:

```sql
CREATE TABLE <catalog_name>.default.<table_name> (
    device_name STRING,
    temp INT,
    humidity BIGINT
)
USING DELTA;
```

Replace `<catalog_name>` with your catalog name (e.g., `main`).

### 3. Create a Service Principal

1. Navigate to **Settings > Identity and Access** in your Databricks workspace
2. Click **Service principals** and create a new service principal
3. Generate a new secret for the service principal and save it securely
4. Grant the following permissions:
   - `USE_CATALOG` on the catalog (e.g., `main`)
   - `USE_SCHEMA` on the schema (e.g., `default`)
   - `MODIFY` and `SELECT` on the table

Grant permissions using SQL:

```sql
-- Grant catalog permission
GRANT USE CATALOG ON CATALOG <catalog_name> TO `<service-principal-application-id>`;

-- Grant schema permission
GRANT USE SCHEMA ON SCHEMA <catalog_name>.default TO `<service-principal-application-id>`;

-- Grant table permissions
GRANT SELECT, MODIFY ON TABLE <catalog_name>.default.<table_name> TO `<service-principal-application-id>`;
```

The service principal's **Application ID** is your OAuth **Client ID**, and the generated secret is your **Client Secret**.

## Ingestion APIs

Pick the record format that matches your data.

- JSON: schema-free ingestion. Pass a JSON string or a native object (dict, map, and so on) and the SDK serializes it. No compilation step. Good for getting started or dynamic schemas.
- Protocol Buffers: strongly-typed, schema-validated ingestion. More compact on the wire than JSON. A typical choice for production workloads that are not already producing Arrow.
- Avro (beta): row-oriented binary encoding against a declared writer schema. Pass a record object or pre-encoded Avro bytes. Currently available in the Rust, Python, Java, and TypeScript SDKs; support in the other SDKs is in development.
- Arrow Flight: Apache Arrow `RecordBatch` data over the Arrow Flight protocol. Best when the workload is columnar or batched, or the application already produces Arrow (pyarrow, [arrow-rs](https://github.com/apache/arrow-rs), DataFusion, Polars).

JSON, Protocol Buffers, and Avro use one row-based stream API; Arrow Flight is a separate columnar API. Availability per SDK is below — Avro is beta and still rolling out.

| SDK | JSON / Protobuf | Avro (beta) | Arrow Flight |
| --- | --- | --- | --- |
| Rust | Available | Beta | Available since 2.8.0 |
| Python | Available | Beta | Available since 1.8.0 |
| Go (cgo) | Available | In development | Available since 1.6.0 |
| Pure Go | Available | In development | Not available |
| TypeScript | Available | Beta | Available since 1.3.0 |
| Java | Available | Beta | Available since 1.6.0 |
| C++ | Available | In development | Available since 0.3.0 |
| .NET (C#) | Available | In development | Not available |

### JSON and Protocol Buffers ingestion

Records are sent as JSON or Protocol Buffers on the same stream API.

For Protocol Buffers, use `proto2` syntax with `optional` fields so nullable Delta table columns are represented correctly. Instead of writing `.proto` files by hand, each SDK ships a tool that generates a protobuf schema from an existing Unity Catalog table. See the individual SDK READMEs for language-specific usage.

### Avro ingestion (beta)

Send records encoded against a declared Avro writer schema on the same row-based stream API — pass a record object the SDK encodes against the schema, or pre-encoded Avro bytes. Currently available in the Rust, Python, Java, and TypeScript SDKs; support in the other SDKs is in development. The Java SDK's Avro support requires Java 11+ and the `org.apache.avro:avro` dependency. See each SDK's README for language-specific usage.

### Arrow Flight ingestion

Send Apache Arrow `RecordBatch` data directly to Zerobus. A good fit when:

- The workload is naturally columnar or batched — analytics pipelines, gateways aggregating short windows of rows, wide or numeric schemas where row-by-row serialization adds noticeable CPU overhead.
- The application already produces Arrow data — pyarrow, the [arrow-rs](https://github.com/apache/arrow-rs) crates, DataFusion, Polars, or other libraries built on Arrow.

For sparse, one-row-at-a-time traffic, JSON or Protocol Buffers are usually simpler. Most SDKs that expose Arrow Flight ship a runnable `examples/arrow/` directory; see each SDK's README for details.

### Type mappings

Delta column types map to Arrow and proto2 as shown below. JSON is not a typed mapping: objects use the same logical types as the table, and the SDK serializes them without a compiled schema.

For Protocol Buffers, declare fields `optional` when the Delta column is nullable.

| Delta Type | Arrow Type | Proto2 Type |
| --- | --- | --- |
| TINYINT, BYTE | `Int8` | `int32` |
| SMALLINT, SHORT | `Int16` | `int32` |
| INT | `Int32` | `int32` |
| BIGINT, LONG | `Int64` | `int64` |
| FLOAT | `Float32` | `float` |
| DOUBLE | `Float64` | `double` |
| STRING, VARCHAR | `LargeUtf8` | `string` |
| BOOLEAN | `Boolean` | `bool` |
| BINARY | `LargeBinary` | `bytes` |
| DECIMAL | `LargeUtf8` | `string` |
| DATE | `Date32` | `int32` (days since Unix epoch) |
| TIMESTAMP | `Timestamp(Microsecond, UTC)` | `int64` (microseconds since Unix epoch) |
| TIMESTAMP_NTZ | `Timestamp(Microsecond)` (no timezone) | `int64` (microseconds since Unix epoch) |
| ARRAY\<type\> | `List` (item field `item`) | `repeated` type |
| MAP\<key, value\> | `Map` (entries field `entries` with `keys` and `values`) | `map<key, value>` |
| STRUCT\<fields\> | nested struct | nested message |
| VARIANT | struct of `metadata` and `value`, both non-null `LargeBinary` | `string` (JSON) |

DECIMAL is encoded as text on both paths today (`LargeUtf8` / `string`). STRING maps to Arrow `LargeUtf8`, not `Utf8`.

### Acknowledgments and throughput

Ingestion is asynchronous in every SDK. An `ingest` call returns as soon as the record is queued — the SDK sends it and tracks its acknowledgment on a background task. To confirm that records were durably committed, call `flush()`; it returns once everything queued so far has been acknowledged.

The idiomatic flow is therefore **ingest in a loop, then `flush()`** — once at the end of a bounded batch, or periodically for a long-running stream. Where the SDK supports it, you can instead register an ack callback and be notified as records commit, without blocking at all.

Each `ingest` also returns the record's offset, and `wait_for_offset(offset)` blocks until that offset is acknowledged. That's useful when a particular record must be confirmed before you continue; because acknowledgments are ordered, waiting on the last offset of a run confirms the whole run. The one thing to avoid is waiting on every record inside a tight loop — that turns the asynchronous pipeline into a synchronous request/response and limits throughput to a single record per network round-trip.

See each SDK's README for exact method names and a runnable example.

## HTTP Proxy Support

All SDKs support HTTP CONNECT proxies via environment variables, following gRPC core conventions. The first variable found (in order) is used:

| Proxy                         | No-proxy                          |
| ----------------------------- | --------------------------------- |
| `grpc_proxy` / `GRPC_PROXY`   | `no_grpc_proxy` / `NO_GRPC_PROXY` |
| `https_proxy` / `HTTPS_PROXY` | `no_proxy` / `NO_PROXY`           |
| `http_proxy` / `HTTP_PROXY`   |                                   |

The `no_proxy` value is a comma-separated list of hostnames (suffix-matched) or `*` to bypass the proxy entirely.

```bash
export https_proxy=http://my-proxy:8080
export no_proxy=localhost,127.0.0.1
```

The SDK establishes a plaintext HTTP CONNECT tunnel through the proxy, then performs a TLS handshake end-to-end with the Databricks server. The proxy never sees decrypted traffic.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Each SDK also has its own contributing guide with language-specific setup instructions.

## License

This project is licensed under the Apache License 2.0. See [LICENSE](LICENSE) for the full text.

---

<!-- tech-stack-wall -->
## Tech Stack

<div align="center">

<img src="https://img.shields.io/badge/Rust-dea584?style=for-the-badge&logo=rust&logoColor=black" alt="Rust" />
<img src="https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white" alt="Databricks" />

</div>

<details>
<summary><b>Full Tech Stack Wall</b></summary>
<br>

<div align="center">

<b>Languages</b><br>
<img src="https://img.shields.io/badge/Rust-dea584?style=for-the-badge&logo=rust&logoColor=black" alt="Rust" />
<img src="https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white" alt="Go" />
<img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript" />
<img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript" />
<img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" alt="Java" />
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
<img src="https://img.shields.io/badge/C-A8B9CC?style=for-the-badge&logo=c&logoColor=black" alt="C" />
<img src="https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=cplusplus&logoColor=white" alt="C++" />
<img src="https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white" alt="Kotlin" />
<img src="https://img.shields.io/badge/Swift-F05138?style=for-the-badge&logo=swift&logoColor=white" alt="Swift" />
<img src="https://img.shields.io/badge/Ruby-CC342D?style=for-the-badge&logo=ruby&logoColor=white" alt="Ruby" />
<img src="https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white" alt="PHP" />
<img src="https://img.shields.io/badge/Lua-2C2D72?style=for-the-badge&logo=lua&logoColor=white" alt="Lua" />
<img src="https://img.shields.io/badge/Shell-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white" alt="Shell" />
<br><br>
<b>Frontend &amp; Desktop</b><br>
<img src="https://img.shields.io/badge/Vue-4FC08D?style=for-the-badge&logo=vuedotjs&logoColor=black" alt="Vue" />
<img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React" />
<img src="https://img.shields.io/badge/Svelte-FF3E00?style=for-the-badge&logo=svelte&logoColor=white" alt="Svelte" />
<img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white" alt="Next.js" />
<img src="https://img.shields.io/badge/Nuxt-00DC82?style=for-the-badge&logo=nuxtdotjs&logoColor=black" alt="Nuxt" />
<img src="https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white" alt="Flutter" />
<img src="https://img.shields.io/badge/React%20Native-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React Native" />
<img src="https://img.shields.io/badge/Tauri-FFC131?style=for-the-badge&logo=tauri&logoColor=black" alt="Tauri" />
<img src="https://img.shields.io/badge/Electron-47848F?style=for-the-badge&logo=electron&logoColor=white" alt="Electron" />
<img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite" />
<img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5" />
<img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3" />
<img src="https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=white" alt="Sass" />
<img src="https://img.shields.io/badge/Less-1D365D?style=for-the-badge&logo=less&logoColor=white" alt="Less" />
<img src="https://img.shields.io/badge/Tailwind%20CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white" alt="Tailwind CSS" />
<img src="https://img.shields.io/badge/Bootstrap-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white" alt="Bootstrap" />
<img src="https://img.shields.io/badge/Three.js-000000?style=for-the-badge&logo=threedotjs&logoColor=white" alt="Three.js" />
<img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white" alt="Node.js" />
<img src="https://img.shields.io/badge/jQuery-0769AD?style=for-the-badge&logo=jquery&logoColor=white" alt="jQuery" />
<br><br>
<b>Database &amp; Storage</b><br>
<img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL" />
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL" />
<img src="https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white" alt="SQLite" />
<img src="https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white" alt="SQL Server" />
<img src="https://img.shields.io/badge/Oracle-F80000?style=for-the-badge&logo=oracle&logoColor=white" alt="Oracle" />
<img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white" alt="Redis" />
<img src="https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white" alt="MongoDB" />
<img src="https://img.shields.io/badge/DuckDB-FFCB00?style=for-the-badge&logo=duckdb&logoColor=black" alt="DuckDB" />
<img src="https://img.shields.io/badge/ClickHouse-FFCC00?style=for-the-badge&logo=clickhouse&logoColor=black" alt="ClickHouse" />
<img src="https://img.shields.io/badge/Elasticsearch-005571?style=for-the-badge&logo=elasticsearch&logoColor=white" alt="Elasticsearch" />
<img src="https://img.shields.io/badge/Neo4j-008CC1?style=for-the-badge&logo=neo4j&logoColor=white" alt="Neo4j" />
<img src="https://img.shields.io/badge/InfluxDB-22ADF6?style=for-the-badge&logo=influxdb&logoColor=white" alt="InfluxDB" />
<img src="https://img.shields.io/badge/Cassandra-1287B1?style=for-the-badge&logo=apachecassandra&logoColor=white" alt="Cassandra" />
<img src="https://img.shields.io/badge/DynamoDB-4053D6?style=for-the-badge&logo=amazondynamodb&logoColor=white" alt="DynamoDB" />
<img src="https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black" alt="Firebase" />
<img src="https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=black" alt="Supabase" />
<img src="https://img.shields.io/badge/MinIO-C72E49?style=for-the-badge&logo=minio&logoColor=white" alt="MinIO" />
<img src="https://img.shields.io/badge/Firebird-FC521F?style=for-the-badge" alt="Firebird" />
<img src="https://img.shields.io/badge/IBM%20DB2-1F70C1?style=for-the-badge" alt="IBM DB2" />
<img src="https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white" alt="MariaDB" />
<img src="https://img.shields.io/badge/CockroachDB-7B52C0?style=for-the-badge" alt="CockroachDB" />
<img src="https://img.shields.io/badge/IRIS-3B82F6?style=for-the-badge" alt="IRIS" />
<img src="https://img.shields.io/badge/Databricks%20SQL-FF3621?style=for-the-badge&logo=databricks&logoColor=white" alt="Databricks SQL" />
<img src="https://img.shields.io/badge/Snowflake-29B5E8?style=for-the-badge&logo=snowflake&logoColor=white" alt="Snowflake" />
<img src="https://img.shields.io/badge/Qdrant-DC244C?style=for-the-badge" alt="Qdrant" />
<img src="https://img.shields.io/badge/Redshift-8C4FFF?style=for-the-badge&logo=amazonredshift&logoColor=white" alt="Redshift" />
<img src="https://img.shields.io/badge/Apache%20Kylin-F59E0B?style=for-the-badge" alt="Apache Kylin" />
<img src="https://img.shields.io/badge/BigQuery-4285F4?style=for-the-badge&logo=googlebigquery&logoColor=white" alt="BigQuery" />
<img src="https://img.shields.io/badge/VictoriaMetrics-3483EB?style=for-the-badge" alt="VictoriaMetrics" />
<img src="https://img.shields.io/badge/Databend-4F46E5?style=for-the-badge" alt="Databend" />
<img src="https://img.shields.io/badge/TDengine-1B8FD4?style=for-the-badge" alt="TDengine" />
<img src="https://img.shields.io/badge/Teradata-0055A6?style=for-the-badge" alt="Teradata" />
<br><br>
<b>Messaging &amp; Streaming</b><br>
<img src="https://img.shields.io/badge/Kafka-231F20?style=for-the-badge&logo=apachekafka&logoColor=white" alt="Kafka" />
<img src="https://img.shields.io/badge/RabbitMQ-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white" alt="RabbitMQ" />
<img src="https://img.shields.io/badge/RocketMQ-FF6A00?style=for-the-badge&logoColor=white" alt="RocketMQ" />
<img src="https://img.shields.io/badge/Pulsar-188FFF?style=for-the-badge&logo=apachepulsar&logoColor=white" alt="Pulsar" />
<img src="https://img.shields.io/badge/Flink-E6526F?style=for-the-badge&logo=apacheflink&logoColor=white" alt="Flink" />
<br><br>
<b>DevOps &amp; Cloud Native</b><br>
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
<img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white" alt="Kubernetes" />
<img src="https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white" alt="Terraform" />
<img src="https://img.shields.io/badge/Ansible-EE0000?style=for-the-badge&logo=ansible&logoColor=white" alt="Ansible" />
<img src="https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white" alt="Jenkins" />
<img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white" alt="GitHub Actions" />
<img src="https://img.shields.io/badge/GitLab%20CI-FC6D26?style=for-the-badge&logo=gitlab&logoColor=white" alt="GitLab CI" />
<img src="https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white" alt="Prometheus" />
<img src="https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white" alt="Grafana" />
<img src="https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white" alt="Nginx" />
<img src="https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white" alt="AWS" />
<img src="https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" alt="Azure" />
<img src="https://img.shields.io/badge/Cloudflare-F38020?style=for-the-badge&logo=cloudflare&logoColor=white" alt="Cloudflare" />
<br><br>
<b>Tools &amp; Platforms</b><br>
<img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white" alt="Git" />
<img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux" />
<img src="https://img.shields.io/badge/macOS-000000?style=for-the-badge&logo=apple&logoColor=white" alt="macOS" />
<img src="https://img.shields.io/badge/VS%20Code-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white" alt="VS Code" />
<img src="https://img.shields.io/badge/Vim-019733?style=for-the-badge&logo=vim&logoColor=white" alt="Vim" />
<img src="https://img.shields.io/badge/Tmux-1BB91F?style=for-the-badge&logoColor=white" alt="Tmux" />
<img src="https://img.shields.io/badge/Homebrew-FAB316?style=for-the-badge&logo=homebrew&logoColor=black" alt="Homebrew" />
<img src="https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white" alt="Postman" />
<img src="https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white" alt="Figma" />
<img src="https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white" alt="Markdown" />
<img src="https://img.shields.io/badge/Maven-C71A36?style=for-the-badge&logo=apachemaven&logoColor=white" alt="Maven" />
<img src="https://img.shields.io/badge/Gradle-02303A?style=for-the-badge&logo=gradle&logoColor=white" alt="Gradle" />
<img src="https://img.shields.io/badge/CMake-064F8C?style=for-the-badge&logo=cmake&logoColor=white" alt="CMake" />

</div>
</details>

<div align="center">
<sub>Hands-on engineering, built and documented in the open.</sub>
</div>

---

<!-- dbx-connections -->
## DBX Connections

<div align="center">

<img src="https://img.shields.io/badge/Firebird_5n1b-DBX-FC521F?style=flat-square" alt="Firebird_5n1b" />
<img src="https://img.shields.io/badge/JDBCX_d5pn-DBX-6D28D9?style=flat-square" alt="JDBCX_d5pn" />
<img src="https://img.shields.io/badge/IBM%20DB2_0leg-DBX-1F70C1?style=flat-square" alt="IBM DB2_0leg" />
<img src="https://img.shields.io/badge/MariaDB_80g9-DBX-003545?style=flat-square" alt="MariaDB_80g9" />
<img src="https://img.shields.io/badge/SQL%20Server_wieh-DBX-CC2927?style=flat-square" alt="SQL Server_wieh" />
<img src="https://img.shields.io/badge/CockroachDB_mo9c-DBX-7B52C0?style=flat-square" alt="CockroachDB_mo9c" />
<img src="https://img.shields.io/badge/IRIS_cz3h-DBX-3B82F6?style=flat-square" alt="IRIS_cz3h" />
<img src="https://img.shields.io/badge/Databricks_SQL_rmue-DBX-FF3621?style=flat-square" alt="Databricks_SQL_rmue" />
<img src="https://img.shields.io/badge/Snowflake_cm_h9-DBX-29B5E8?style=flat-square" alt="Snowflake_cm_h9" />
<img src="https://img.shields.io/badge/Redis_u0tv-DBX-DC382D?style=flat-square" alt="Redis_u0tv" />
<img src="https://img.shields.io/badge/Qdrant_1r3s-DBX-DC244C?style=flat-square" alt="Qdrant_1r3s" />
<img src="https://img.shields.io/badge/Elasticsearch_zfc3-DBX-005571?style=flat-square" alt="Elasticsearch_zfc3" />
<img src="https://img.shields.io/badge/Cassandra_d8eb-DBX-1287B1?style=flat-square" alt="Cassandra_d8eb" />
<img src="https://img.shields.io/badge/MongoDB_vexq-DBX-47A248?style=flat-square" alt="MongoDB_vexq" />
<img src="https://img.shields.io/badge/Redshift_p9d7-DBX-8C4FFF?style=flat-square" alt="Redshift_p9d7" />
<img src="https://img.shields.io/badge/Apache%20Kylin_xmpz-DBX-F59E0B?style=flat-square" alt="Apache Kylin_xmpz" />
<img src="https://img.shields.io/badge/Neo4j_j3dsg-DBX-008CC1?style=flat-square" alt="Neo4j_j3dsg" />
<img src="https://img.shields.io/badge/BigQuery_homk-DBX-4285F4?style=flat-square" alt="BigQuery_homk" />
<img src="https://img.shields.io/badge/Apache%20Kafka_xpqk-DBX-231F20?style=flat-square" alt="Apache Kafka_xpqk" />
<img src="https://img.shields.io/badge/VictoriaMetrics_m3sf-DBX-3483EB?style=flat-square" alt="VictoriaMetrics_m3sf" />
<img src="https://img.shields.io/badge/InfluxDB_wuju-DBX-22ADF6?style=flat-square" alt="InfluxDB_wuju" />
<img src="https://img.shields.io/badge/Databend_dey6-DBX-4F46E5?style=flat-square" alt="Databend_dey6" />
<img src="https://img.shields.io/badge/TDengine_4c9i-DBX-1B8FD4?style=flat-square" alt="TDengine_4c9i" />
<img src="https://img.shields.io/badge/Teradata_rwlm-DBX-0055A6?style=flat-square" alt="Teradata_rwlm" />

</div>

<sub>Connection names shown in the DBX sidebar - decorative reference badges.</sub>
