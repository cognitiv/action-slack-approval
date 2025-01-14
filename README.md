# slack-approval

custom action to send approval request to Slack

![](https://user-images.githubusercontent.com/35091584/195488201-acc24277-5e0c-431f-a4b3-21b4430d5d80.png)

- Post a message in Slack with a "Approve" and "Reject" buttons.
- Clicking on "Approve" will execute next steps.
- Clicking on "Reject" will cause workflow to fail.

# How To Use

- First, create a Slack App and install in your workspace.
- Second, add `chat:write` and `im:write` to OAuth Scope on OAuth & Permissions page.
- Finally, **Enable Socket Mode**.

```
jobs:
  approval:
    runs-on: ubuntu-latest
    steps:
      - name: send approval
        uses: Precise-Finance/slack-approval@v1
        env:
          SLACK_APP_TOKEN: ${{ secrets.SLACK_APP_TOKEN }}
          SLACK_BOT_TOKEN: ${{ secrets.SLACK_BOT_TOKEN }}
          SLACK_SIGNING_SECRET: ${{ secrets.SLACK_SIGNING_SECRET }}
          SLACK_CHANNEL_ID: ${{ secrets.SLACK_CHANNEL_ID }}
        timeout-minutes: 10
```

- Set environment variables

  - `SLACK_APP_TOKEN`

    - App-level tokens on `Basic Information page`. (starting with `xapp-` )

  - `SLACK_BOT_TOKEN`

    - Bot-level tokens on `OAuth & Permissions page`. (starting with `xoxb-` )

  - `SLACK_SIGNING_SECRET`

    - Signing Secret on `Basic Information page`.

  - `SLACK_CHANNEL_ID`

    - Channel ID for which you want to send approval.

- Set `timeout-minutes`
  - Set the time to wait for approval.

## Contributing

Since this is typescript, it depends on Node and NPM. I recommend installing via the [Node Version Manager](https://github.com/nvm-sh/nvm)

### Install Dependencies

```bash
npm install
```

### Editing

Most of this code is a single file, in [index.ts](./src/index.ts). This code will be transpiled and bundled into the deliverable [index.js](./dist/index.js).

_While it is not required to bundle dependencies, I found GitHub actions were a bit flakey in finding them. Bundling removes that issue completely_.

### Compiling

```build
npm run build
```

### Deploying

Deploying is as simple as making sure the `main` branch is up to date. When you are happy with your changes, merge into main.
