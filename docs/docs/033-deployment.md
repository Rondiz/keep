---
sidebar_label: Deployment
---

# 🫸 Deployment

After writing some alerts with Keep, you may now want to use Keep in production! For that, you can easily deploy Keep on an environment other than your local station.

Keep currently supports [Docker](#docker) and [Render](#render).
:::warning Missing something?
 Want to deploy Keep on a specific platform that is not yet supported? [Just open an issue](https://github.com/keephq/keep/issues/new?assignees=&labels=&template=feature_request.md&title=feature:%20new%20deployment%20option) and we will get to it ASAP!
:::

## E2E

### Docker

## CLI

Run *Keep* alerting engine (The CLI)

### Docker

Configure the Slack provider (See "[Run locally](https://github.com/keephq/keep#get-a-slack-incoming-webhook-using-this-tutorial-and-use-keep-to-configure-it)" on how to obtain the webhook URL)

```bash
docker run -v ${PWD}:/app -it keephq/cli config provider --provider-type slack --provider-id slack-demo
```

You should now have a providers.yaml file created locally

Run Keep and execute our example "Paper DB has insufficient disk space" alert

```bash
docker run -v ${PWD}:/app -it keephq/cli -j run --alert-url https://raw.githubusercontent.com/keephq/keep/main/examples/alerts/db_disk_space.yml
```

### Render
Click the Deploy to Render button to deploy Keep as a background worker running in [Render](https://www.render.com)

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/keephq/keep)

To run Keep and execute our example "Paper DB has insufficient disk space" alert, you will need to configure you Slack provider.
When clicking the Deploy to Render button, you will be asked to provide the `KEEP_PROVIDER_SLACK_DEMO` environment variable, this is the expected format:

```json
{"authentication": {"webhook_url": "https://hooks.slack.com/services/..."}}
```

\** `KEEP_PROVIDER_PROVIDER_ID` is the way you can configure providers using environment variables <br/>
\** Refer to [Run locally](https://github.com/keephq/keep#get-a-slack-incoming-webhook-using-this-tutorial-and-use-keep-to-configure-it) on how to obtain a Slack webhook URL or on how to obtain Keep's webhook.
