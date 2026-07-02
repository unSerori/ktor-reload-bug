# ktor reload bug

Sample repository for reproducing the [Ktor Issue](#????).

## Specification

Create new project on [start.ktor.io](https://start.ktor.io/) with the following settings:

- Build system: Gradle
- Engine: Netty
- Configuration: HOCON File
- No plugins

Configured Auto-reload according to [Auto-reload | Ktor Documentation](https://ktor.io/docs/server-auto-reload.html).
Adopted the following format:

- EngineMain
- application.conf

## How to Start

1. `cp .env.example .env`
2. `docker compose up --build -d`

Each service can also be started individually:

- `docker compose run --rm --service-ports ktor-v3_4_3`
- `docker compose run --rm --service-ports ktor-v3_5_0`
