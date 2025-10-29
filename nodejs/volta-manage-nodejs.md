# Volta で Node.js のバージョンを管理する

## 目的
Volta で Node.js の導入状況を確認し、最新 LTS の追加と不要なバージョン整理を最小の手順で行う。

## 手順

### インストール済みバージョンを確認する
- 端末で `volta list node` を実行し、デフォルト・現在利用中のバージョンを把握する。

```bash
volta list node
```

### 最新 LTS をインストールする
- 最新 LTS を導入する場合は `volta install node@lts` を実行する。インストール後は自動でデフォルトに設定される。

```bash
volta install node@lts
```

### 古いバージョンを削除する
1. `volta list node` で不要なバージョン (例: `22.20.0`) を確認する。
2. Volta にはバージョンごとのアンインストールコマンドがないため、`$VOLTA_HOME` 配下のキャッシュを手動で削除する。`VOLTA_HOME` の既定値は `~/.volta`。

```bash
rm -r "$VOLTA_HOME/tools/image/node/22.20.0"
rm "$VOLTA_HOME/tools/inventory/node/node-v22.20.0-darwin-arm64.tar.gz"
rm "$VOLTA_HOME/tools/inventory/node/node-v22.20.0-npm"
```

## 注意点
- 削除対象のバージョンを利用しているプロジェクトがないか事前に確認する。
- `VOLTA_HOME` をカスタム設定している場合、各パスを読み替える。
