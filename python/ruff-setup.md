# ruffのセットアップ

## ruffのインストール

開発用の依存にruffをインストールします

```shell
# 例)
uv add --group dev ruff
```

## 設定

pyproject.tomlに以下の内容をコメントも含めて追記します。

```toml
[tool.ruff]
line-length = 88
indent-width = 4
target-version = "py314"
force-exclude = true

[tool.ruff.lint]
select = [
    "F",    # Pyflakes 相当: 未使用変数など
    "E",    # pycodestyle errors
    "W",    # pycodestyle warnings
    "C90",  # mccabe: 複雑度
    "I",    # isort 相当(import並び)
    "N",    # pep8-naming: 名前付け規約
    "B",    # flake8-bugbear: バグっぽいコード検出
    "S",    # flake8-bandit: セキュリティ
    "C4",   # flake8-comprehensions: 内包表記の改善
    "UP",   # pyupgrade: 新しい構文への置き換え
]

# formatterと衝突する/したときにノイズになるルールを ignore に追加
# これらはRuff公式が「formatterと一緒に使うなら無効にして」と案内している
# COM812, COM819: カンマ位置・末尾カンマ
# ISC001: 暗黙の文字列結合
# W191, E111, E114, E117: インデント / 空白
# D206, D300: docstringの引用符・インデント
# Q000〜Q003: クォート統一
ignore = [
    "E501", # line-too-long: フォーマッタで調整できない場合は無視する(settingsやURLなど)
    # formatterと衝突する/したときにノイズになるルール
    "W191", "E111", "E114", "E117",  # インデント系
    "D206", "D300",                  # docstring のクォート/インデント
    "Q000", "Q001", "Q002", "Q003",  # クォートスタイル強制
    "COM812", "COM819",              # 末尾カンマ関連
    "ISC001",                        # 暗黙の文字列結合
]

# 途中の作業中コードを勝手に消されないようにする
unfixable = [
    "F401", # unused import
    "F841", # unused variable
]

[tool.ruff.lint.per-file-ignores]
"tests/**" = ["S101"]  # テストではassertを許す

[tool.ruff.format]
# フォーマッターの設定はdefaultを使用するため、何も設定しない
```

## プロジェクトのAGENTS.mdに追記

プロジェクトのAGENTS.mdにruffの使用方法がない場合は、以下の内容をAGENTS.mdに追記します

```markdown
コードを変更した場合はruffを実行してください。

uv run ruff check --fix
uv run ruff format
```