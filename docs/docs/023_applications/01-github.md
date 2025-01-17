---
sidebar_label: GitHub
sidebar_position: 1
---

# GitHub Application

The Keep GitHub Application is a powerful tool that enhances your workflow by monitoring file changes under the parent `.keep/` directory in your repositories' pull requests. It automates the process of generating AI-generated alerts from plain English and allows you to seamlessly deploy these alerts to your provider using comments.

## Getting Started

To start using the Keep GitHub Application, follow these simple steps:

1. Sign up and log in to the **[Keep's platform](https://platform.keephq.dev)**.
2. Install the **Keep GitHub Application** either through the onboarding screen or by visiting **[this link](https://github.com/apps/keephq)**. The installation process is straightforward and user-friendly.
   ![GitHub App Installation](/img/github-app-install.png)
3. Connect your preferred provider, such as Datadog, by linking it to Keep's platform. This step allows Keep to seamlessly generate and deploy alerts to your chosen provider.
   ![Connect Provider](/img/connect-provider.png)
4. You are now ready to go! The Keep GitHub Application is successfully integrated into your GitHub workflow.

## How does it work?
The Keep GitHub Application operates seamlessly in the background, ensuring that you stay informed about relevant changes in your repositories. Whenever a pull request is opened or updated, the application monitors the files under the .keep/ directory.

Once a change is detected, the GitHub application sends an HTTP request to Keep's API smart AI layer. The AI layer analyzes the content of the changed files and together with context from the provider (existing alerts, sample logs, etc.) generates an alert based on the user provided plain English description. The AI-powered alert generation ensures accuracy and relevance.

After the alert is generated, the Keep GitHub Application automatically comments the alert on the respective file within the pull request. This allows you, as the user, to conveniently review and verify the generated alert.

If the generated alert meets your requirements and is ready to be deployed, you can simply leave a comment on the file. The comment should include one of the predefined emojis, such as :rocket: or :ok: (refer to the ["Deploying Alerts with Emojis"](#deploying-alerts-with-emojis) section). The Keep GitHub Application recognizes these emojis as commands to proceed with the deployment process.

This intuitive workflow streamlines the alert generation and deployment process, providing you with a seamless experience and allowing you to focus on the core aspects of your project.

## Monitoring Files Under .keep/ Directory

The Keep GitHub Application actively monitors the files residing within the `.keep/` directory located at the parent level of your repository. Any changes or updates made to these files will trigger the alert generation process. This allows you to focus on the essential aspects of your project while ensuring that relevant changes are promptly identified and acted upon.

## Alert File Structure

Each file under the `.keep/` directory represents a single alert. The structure of an alert file follows the YAML format. Below is an example of an alert file:

```yaml title=alert-example.yaml
# The alert text in plain English
alert: |
    Count the error rate (4xx-5xx) this service has in the last 10 minutes.
    Alert when the threshold is above 5% out of total requests.
    Send a Slack message to the #alerts-playground channel and include all the context you have"

# The provider you've previously connected and want this alert to be generated for
provider: datadog

# You can use this to override Keep's managed API and have the GitHub application
# use the API that you run locally (using the NGROK URL)
# api_url: https://OVERRIDE-KEEP-MANAGED-API
```

The alert file consists of the following components:

1. **Alert Text**: This section contains the plain English description of the alert. Write a clear and concise explanation of the conditions or criteria that should trigger the alert. You can include any relevant context to facilitate understanding and resolution.

2. **Provider**: Specify the provider to which you want the alert to be generated. This ensures that the alert seamlessly integrates with your existing monitoring and notification infrastructure. In the example above, the alert is configured to be generated for Datadog.

3. **API Override**: Optionally, you can include the api_url field to override Keep's managed API. This allows you to use your locally hosted API for advanced customization and integration purposes.

<details>
  <summary>ngrok</summary>
  <div>

<b>ngrok?</b>

Imagine you have a secret hideout in your backyard, but you don't want anyone to know where it is. So, you build a tunnel from your hideout to a tree in your friend's backyard. This way, you can go into the tunnel in your yard and magically come out at the tree in your friend's yard.

Now, let's say you have a cool website or a game that you want to show your friend, but it's running on your computer at home. Your friend is far away and can't come to your house. So, you need a way to show them your website or game over the internet.

This is where ngrok comes in! Ngrok is like a magical tunnel, just like the one you built in your backyard. It creates a secure connection between your computer and the internet. It gives your computer a special address that people can use to reach your website or game, even though it's on your computer at home.

When you start ngrok, it opens up a tunnel between your computer and the internet. It assigns a special address to your computer, like a secret door to your website or game. When your friend enters that address in their web browser, it's as if they're walking through the tunnel and reaching your website or game on your computer.

So, ngrok is like a magical tunnel that helps you share your website or game with others over the internet, just like the secret tunnel you built to reach your friend's backyard!

<b>How to start Keep with ngrok?</b>

ngrok is Controlled with the `USE_NGROK` environment variable.<br />
Simply run Keep's API using the following command to start with ngrok: `USE_NGROK=true keep api`

:::note
`USE_NGROK` is enabled by default when running with `docker-compose`
:::

<b>How to obtain ngrok URL?</b>

When `USE_NGROK` is set, Keep will start with ngrok in the background. <br />
You can find your private ngrok URL looking for this log line "`ngrok tunnel`":
```json
{
    "asctime": "0000-00-00 00:00:00,000",
    "message": "ngrok tunnel: https://fab5-213-57-123-130.ngrok.io",
    ...
}
```
The URL (https://fab5-213-57-123-130.ngrok.io in the example above) is a publicly accessible URL to your Keep API service running locally. <br />
:::note
You can check that the ngrok tunnel is working properly by sending a simple HTTP GET request to `/healthcheck`<br />
Try: `curl -v https://fab5-213-57-123-130.ngrok.io/healthcheck` in our example.
:::
  </div>
</details>

## Deploying Alerts with Emojis
To deploy an alert to the specified provider, you can simply leave a comment on the respective file using the :rocket: or :ok: emojis. The Keep GitHub Application recognizes these emojis as commands and will initiate the deployment process accordingly. This streamlined approach ensures a smooth and intuitive experience when deploying alerts.

For example, by leaving a comment with the :rocket: emoji, you can signal the Keep GitHub Application to deploy the alert to the specified provider (Datadog in our example above).

![Generated Example](/img/first-alert.yaml.png)

The Keep GitHub Application will either mark the comment with :+1: meaning the alert was successfully deployed or :-1: and another comment with the failure reason in case the alert was not deployed.

:::note
Keep GitHub Application has a retry mechanism that automatically tries to fix the alert in case it was not successfully deployed to the provider.
If the alert that is deployed is different from the originally generated one, Keep Github Application will comment the updated one once again.
:::
