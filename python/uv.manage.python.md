3.13.xを3.13.y(3.13の中で現在最新のパッチバージョン)にしたい時

```shell
# インストール可能な最新バージョンを確認する
uv python list

# 3.13のうち最新のパッチバージョンにアップグレードする
uv python upgrade 3.13

# 3.13の古いパッチバージョンをアンインストールする
uv python uninstall 3.13.x

# インストール結果を確認する
uv python list --only-installed
```