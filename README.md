# remote-instructions

このリポジトリはコーディングエージェント用のinstructionを管理しています。

フォルダ構成

- python
  - Pythonに関するインストラクション集
- node
  - Node.jsに関するインストラクション集


For Agents,

おそらくサンドボックス環境ではエラーになるので、ユーザーにサンドボックスの外で実行して良いか確認してください。

## ls

```shell
gh api "/repos/ekozmdev/remote-instructions/contents/{dir_name}?ref=main" --jq '.[] | {name, url: .url}'
```

<!-- TODO アクセストークンアリの場合も書く -->

```shell
curl -fsS \
  -H "Accept: application/vnd.github+json" \
  "https://api.github.com/repos/ekozmdev/remote-instructions/contents/{dir_name}?ref=main" \
| jq -r '.[] | {name, url: .url}'
```

## cat

```shell
gh api -H "Accept: application/vnd.github.raw" "/repos/ekozmdev/remote-instructions/contents/{dir_name}/{file_name}?ref=main"
```

<!-- TODO アクセストークンアリの場合も書く -->

```shell
curl -fsS \
  -H "Accept: application/vnd.github.raw" \
  "https://api.github.com/repos/ekozmdev/remote-instructions/contents/{dir_name}/{file_name}?ref=main"
```
