# casdoor-deploy

Casdoor deployment with Docker Compose and SQLite database.

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

Start the Casdoor service:

```bash
docker-compose up -d
```

## Access

Casdoor will be available at http://localhost:8000

## Configuration

The `conf/app.conf` file contains the SQLite database configuration:

- `dataSourceName`: Path to the SQLite database file
- `dbType`: Database type (sqlite3)
