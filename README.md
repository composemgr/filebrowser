## 👋 Welcome to filebrowser 🚀

Web-based file manager with a clean interface

## 📋 Description

Web-based file manager with a clean interface

## 🚀 Services

- **filebrowser**: filebrowser/filebrowser:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/filebrowser/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/filebrowser" ~/.local/srv/docker/filebrowser
cd ~/.local/srv/docker/filebrowser
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install filebrowser
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
SERVICE_USER=1000
SERVICE_GROUP=1000
```

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64170` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64170

## 📂 Volumes

- `./volumes/config/filebrowser` - Application configuration and database
- `./volumes/data/filebrowser` - Served file storage


## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- The `172.17.0.1` bind address limits access to the Docker host gateway only
- Set up HTTPS using a reverse proxy (nginx, traefik, caddy) for production
- Keep regular backups of the database and application data volumes
- Update Docker images regularly to pick up security patches

## 🔍 Logging

```shell
docker compose --env-file .env logs -f filebrowser
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
