これでリポジトリ全体のファイルを一括で取得できる

gh api "/repos/ekozmdev/remote-instructions/git/trees/main?recursive=1" --jq '.tree[] | .path'

README.md
python
python/python-setup.md

絞り込む時は --jqでガンバる
APIのパスは""で囲む

gh api "repos/ekozmdev/remote-instructions/git/trees/main?recursive=1" \
  --jq '.tree[] | select(.path | startswith("python/")) | .path'