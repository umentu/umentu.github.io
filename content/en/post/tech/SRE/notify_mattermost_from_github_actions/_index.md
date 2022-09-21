+++
aliases =["posts", "articles", "blog", "showcase", "docs"]
author = "umentu"
title = "How to notify MATTERMOST of commit contents from GitHub Actions."
date = "2022-08-29"
description = "Learn how to notify MATTERMOST of commit messages from GitHub Actions."
tags =["tech", "SRE"]
+++
1. Get Webhook URL of Mattermost from `Integrations -> Incoming Webhooks`.The Channel to be notified can be any one.
2. The Webhook URL created in step 1 shold be registered in the `GitHub's repository->Settings->Secrets->Actions` under the name `MATTERMOST_NOTION`.
3. Create YAML file under `PROJECT_DIR/.github/workflows` with any name and write the following contents. Branch name are set as appropriate.


```
on:
  push:x
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

4. Once the YAML file is Commit and Push is done, notification is initiated.