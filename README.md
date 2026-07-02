# ktor reload bug

[KtorのIssue](#????)の再現用のサンプルリポジトリ。

## 仕様

start.ktor.ioでプロジェクを作成

- Build system: Gradle
- Engine: Netty
- Configuration: HOCON File
- プラグインなし

そこに[Auto-reload | Ktor Documentation](https://ktor.io/docs/server-auto-reload.html)どおりに設定を行った。
以下の形式を採用

- EngineMain
- application.conf

## 起動方法

1. `cp .env.example .env`
2. `docker compose up --build -d`

起動はそれぞれ個別に行うことも可能

- `docker compose run --rm --service-ports ktor-v3_4_3`
- `docker compose run --rm --service-ports ktor-v3_5_0`
