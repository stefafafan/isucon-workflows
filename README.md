# isucon-workflows
ISUCON向けに導入できる GitHub Reusable Workflows をまとめたリポジトリです。

## 設定例

言語ごとに簡単に導入できるサンプルを提示します。

### Go

以下のようなWorkflowを設定すると内部で golangci-lint を用いてリンターを走らせることができます。

```yaml
name: Go Lint

on:
  pull_request:
    types: [opened, synchronize]
  push:
    branches:
      - main

permissions:
  contents: read
  pull-requests: read

jobs:
  lint:
    uses: stefafafan/isucon-workflows/.github/workflows/golang.yml@v1
    with:
      working-directory: './webapp/go'
```

設定値(それぞれ省略可能)
- **working-directory**: `webapp/go` のディレクトリまでのパスです。デフォルト値は `./webapp/go` です
- **golangci-config**: `.golangci.yml` の設定があればパスを指定できます。デフォルト値は空です (設定ファイルなし)
- **only-new-issues**: 新しい差分のみLintを走らせるかどうかです。デフォルト有効です。

### Node

以下のようなWorkflowを設定すると js ファイルに対して `node --check` を実施させることができます。

```yaml
name: Node Syntax Check

on:
  pull_request:
    types: [opened, synchronize]
  push:
    branches:
      - main

jobs:
  check:
    uses: ./.github/workflows/node.yml
    with:
      working-directory: './webapp/node'
```

設定値(省略可能)
- **working-directory**: `webapp/node` のディレクトリまでのパスです。デフォルト値は `./webapp/node` です。ISUCONでは `nodejs` というディレクトリになっていることもあるので注意。
