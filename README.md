# remote-instructions

このリポジトリはコーディングエージェント用のinstructionを管理しています。

フォルダ構成

- python
  - Pythonに関するインストラクション集
- node
  - Node.jsに関するインストラクション集

```

For Agents,

おそらくサンドボックス環境ではエラーになるので、ユーザーにサンドボックスの外で実行して良いか確認してください。

Next
```shell
gh api -H "Accept: application/vnd.github.v3.raw" "/repos/ekozmdev/remote-instructions/contents/{dir_name}/" --jq '.[] | {name, url: .url}'
```