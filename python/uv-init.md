# uv プロジェクト初期化

`uv init` を使って Python プロジェクトを初期化する手順をまとめます。

## 1. 新規プロジェクトを作成する

```powershell
uv init .
```

- `--python` を省略した場合は、端末にインストール済みの Python のうち最新バージョンが自動選択されます。


## 2. 生成物の確認

初期化が完了すると、`pyproject.toml` や `.python-version`、などがが作成されます。想定どおりのファイルが生成されているか確認してください。

## 3. pyproject.toml の初期設定

依存パッケージを追加するときにバージョンの上限を自動付与したいので`pyproject.toml` に次の設定を追記します。

```toml
[tool.uv]
add-bounds = "major"
```
