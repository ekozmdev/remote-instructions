# uv プロジェクト初期化

`uv init` を使って Python プロジェクトを初期化する手順をまとめます。

## 1. 新規プロジェクトを作成する

```powershell
# 作業用ディレクトリを作成して移動
mkdir uv-sample
cd uv-sample

# プロジェクトを初期化
uv init --python 3.13
```

- `--python` を省略した場合は、端末にインストール済みの Python のうち最新バージョンが自動選択されます。
- 既にディレクトリを用意している場合は、そのディレクトリで `uv init .` を実行すれば同様に初期化できます。

## 2. Git 初期化とブランチ名

`uv init` は内部で `git init` も実行します。初期ブランチ名を `main` に統一したい場合は、あらかじめ次の設定を行ってください。

```powershell
git config --global init.defaultBranch main
```

## 3. 生成物の確認

初期化が完了すると、`pyproject.toml` や `.python-version`、`.venv`（必要に応じて）が作成されます。想定どおりのファイルが生成されているか確認し、必要に応じて README やライセンスファイルを追加してください。

## 4. pyproject.toml の初期設定（任意）

依存パッケージを追加するときにバージョンの上限を自動付与したい場合は、`pyproject.toml` に次の設定を追加します。

```toml
[tool.uv]
add-bounds = "major"
```

- `"major"` は次のメジャーバージョン未満へ制限します。ほかに `"minor"` や `"patch"` なども選択できます。

## 5. 参考リンク

最新の `uv init` オプションや挙動は随時更新されています。詳細は公式ドキュメントを参照してください。  
<https://docs.astral.sh/uv/getting-started/projects/>
