# casdoor-deploy

Casdoor deployment with Docker Compose and PostgreSQL database.

## Prerequisites

- Docker
- Docker Compose

## Setup

1. Create the data and configuration directories on the host:

```bash
mkdir -p /data/app/casdoor/data
mkdir -p /data/app/casdoor/conf
```

2. Copy the `conf/app.conf` configuration file to `/data/app/casdoor/conf/app.conf`:

```bash
cp conf/app.conf /data/app/casdoor/conf/app.conf
```

## Deployment

Start the Casdoor and PostgreSQL services:

```bash
docker-compose up -d
```

## Access

Casdoor will be available at http://localhost:8000

## Configuration

The `conf/app.conf` file contains the PostgreSQL database configuration:

- `dataSourceName`: PostgreSQL connection string
- `dbType`: Database type (postgres)

## PostgreSQL 数据迁移

### 1. 快速备份

在宿主机执行（假设 PostgreSQL 容器名为 `postgres`，数据库名/用户均为 `casdoor`）：

```bash
docker exec -t postgres pg_dump -U casdoor casdoor > casdoor_backup_$(date +%Y%m%d).sql
```

### 2. 快速恢复到同一实例

```bash
cat casdoor_backup_20240101.sql | docker exec -i postgres psql -U casdoor -d casdoor
```

### 3. 迁移到新 PostgreSQL 实例

1. 在旧实例上备份：

```bash
docker exec -t postgres pg_dump -U casdoor casdoor > casdoor_backup.sql
```

2. 在新实例上创建好同名数据库/用户后恢复：

```bash
cat casdoor_backup.sql | docker exec -i NEW_POSTGRES_CONTAINER psql -U casdoor -d casdoor
```

将 `NEW_POSTGRES_CONTAINER` 替换为新 PostgreSQL 容器名即可完成快速迁移。
