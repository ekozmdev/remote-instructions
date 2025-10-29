# uv 日常運用

## 目的

既存の Python プロジェクトで uv を使った仮想環境の運用、依存関係の同期、uv 本体のメンテナンス手順を把握する。

## 手順

1. 仮想環境を自動構築したままコマンドを実行する。
   ```powershell
   uv run main.py
   uv run ruff check
   ```
2. 仮想環境を手動で有効化する必要がある場合は、プロジェクトルートで次を実行する。
   ```powershell
   .\.venv\Scripts\activate
   ```
3. 既存プロジェクトで依存関係と仮想環境を同期する。
   ```powershell
   uv sync
   ```

   - `.python-version` が存在する場合は指定バージョンの Python が利用され、未インストールなら uv が自動取得する。
4. uv 本体をアップデートする。
   ```powershell
   uv self update
   ```
5. キャッシュをクリアしてストレージ空き容量を確保する。
   ```powershell
   uv cache clean
   ```

## 注意点

- `uv run` や `uv sync` は実行時に必要な Python バージョンをチェックするため、複数プロジェクトを並行運用しても仮想環境が衝突しにくい。
- `.python-version` に記載されたバージョンをローカルで未使用の場合、初回同期に時間が掛かる。事前に `uv python install <version>` を実行しておくと短縮できる。
- `uv cache clean` はダウンロード済みアーカイブを削除するため、再インストール時に再取得が発生する点に注意する。
- コマンドの詳細オプションは uv CLI リファレンスで確認する。  
  <https://docs.astral.sh/uv/reference/cli/>
