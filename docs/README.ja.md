<p align="center">
  <a href="">
    <img src="./header.jpg" alt="header" width="100%">
  </a>
  <h1 align="center">Update License Year</h1>
</p>

<p align="center">
  <i>このリポジトリは、GitHub Actions を使用してライセンスファイルの年を更新するプルリクエストを作成するアクションを提供します。</i>
</p>

## 使い方

```yaml
name: Update License Year

on:
  schedule:
    - cron: '0 0 1 1 *' # 毎年1月1日に実行
  workflow_dispatch:

jobs:
  commit-changes:
    runs-on: ubuntu-latest
    timeout-minutes: 5
    permissions:
      contents: write # git push するために必要
    steps:
      - uses: actions/checkout@v4

      - name: Generate GitHub App Token
        id: app_token
        uses: actions/create-github-app-token@v1
        with:
          app-id: ${{ secrets.GHA_APP_ID }}
          private-key: ${{ secrets.GHA_APP_PRIVATE_KEY }}
          owner: ${{ github.repository_owner }}

      - uses: tqer39/update-license-year@v0.0.1-alpha
        with:
          github-token: ${{ steps.app_token.outputs.token }}
```

## inputs

### `github-token`

1. **必須** GitHub トークン。`secrets.GITHUB_TOKEN` ではなく、GitHub App トークンを使用する必要があります。

## 貢献方法

1. このリポジトリをフォークします。
2. 新しいブランチを作成します。
3. 変更を加え、コミットします。
4. プルリクエストを作成します。

## ライセンス

このプロジェクトは [MIT](LICENSE) の下でライセンスされています。
