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
    "B008",   # デフォルト引数での関数呼び出しを許可（FastAPI の Depends() 用）
    "E501",   # 行が長すぎる警告は無視（URL や設定文字列などは折り返さない）

    # formatter と衝突する/したときにノイズになるルール
    "W191",   # タブとスペースが混在したインデント
    "E111",   # インデント幅の不正（スペース数のずれ）
    "E114",   # 予期しないインデント（過剰な字下げ）
    "E117",   # 余分なインデント（不要なネスト風インデント）
    "D206",   # docstring のインデント位置
    "D300",   # docstring のクォート種別（''' / """）統一
    "Q000",   # 文字列リテラルのクォート種別統一
    "Q001",   # docstring のクォート種別統一
    "Q002",   # 複数行文字列のクォート種別統一
    "Q003",   # クォート変更によるエスケープ回避
    "COM812", # 末尾カンマの不足
    "COM819", # 不要な末尾カンマ
    "ISC001", # 暗黙の文字列結合（隣接する文字列リテラルの結合）
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
Pythonコードのlint,formatのためruffを実行してください。

# lint(修正できるものは自動修正)

uv run ruff check --fix

# format

uv run ruff format
```

ruffの実行方法はプロジェクトのパッケージ管理ツールに合わせて、適宜修正する。

## git管理対象外ディレクトリの設定

ruffを実行すると`ruff_cache`ディレクトリが作成されるため、プロジェクトの`.gitignore`に`**/ruff_cache/`を追記する
