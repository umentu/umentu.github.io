+++
aliases =["posts", "articles", "blog", "showcase", "docs"]
author = "umentu"
title = "GitHub ActionsからMattermostにCommit内容を通知する方法"
date = "2022-08-29"
description = "GitHubのCommit内容をMattermostに通知する方法を紹介"
tags =["introduction"]
+++

1. Mattermostの統合機能->内向きのウェブフックからWebhook URLを取得する。通知したいチャンネルを指定する。

2. GitHubのリポジトリの`Settings->Secrets->Actions`を開き、`MATTERMOST_NOTION`という名前で1.で作成したWebhook URLを登録する。

3. `PROJECT_DIR/.github/workflows`配下に任意の名前のYAMLファイルを設置して、以下を記載する。ブランチ名などは適宜設定する。

```
on:
  push:
    branches:
      - "develop"
      - "main"
  pull_request:
    branches:
      - "develop"
      - "main"
    types:
      - "closed"

    

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Create the Mattermost Message
      run: |
        message=`git log -1`
        echo "{\"text\":\"${message}\"}" > mattermost.json
    - uses: mattermost/action-mattermost-notify@master
      env:
        MATTERMOST_WEBHOOK_URL: ${{ secrets.gps }}
```

4. YAMLファイルをCommitしてPushしたら、通知が開始される。