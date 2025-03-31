---
title: "Webhook Setup and Usage"
---

# Webhook Setup and Usage in Gogs

Webhooks allow you to set up integrations which subscribe to certain events in your Gogs repositories. When one of those events is triggered, we'll send a HTTP POST payload to the webhook's configured URL. This guide will walk you through setting up and using webhooks in Gogs.

## Available Events

Gogs supports the following events for webhooks:

- `create`: Branch or tag created
- `delete`: Branch or tag deleted
- `fork`: Repository forked
- `push`: Push to a repository
- `issues`: Issue opened, closed, reopened, edited, assigned, or labeled
- `issue_comment`: Comment added to an issue
- `pull_request`: Pull request opened, closed, reopened, edited, assigned, or labeled
- `release`: Release published in a repository

## Webhook Payload Format

The webhook payload is sent as a POST request with a JSON body. The exact structure of the payload depends on the event type. However, all payloads include some common fields:

- `secret`: The secret you configured for the webhook (if any)
- `ref`: The full Git ref that was pushed
- `repository`: Information about the repository where the event occurred

For detailed information about the payload structure for each event type, please refer to the API documentation.

## Configuring Webhooks

To set up a webhook for your repository:

1. Go to your repository's settings page
2. Click on "Webhooks" in the left sidebar
3. Click "Add webhook"
4. Fill in the webhook details:
   - Payload URL: The URL to which the webhook payload will be sent
   - Content type: application/json or application/x-www-form-urlencoded
   - Secret: A secret string to secure your webhook (optional but recommended)
   - Select the events you want to trigger this webhook
5. Click "Add webhook" to save

### Example: Creating a Webhook via API

You can also create webhooks programmatically using the Gogs API. Here's an example using curl:

```bash
curl -X POST 'https://your-gogs-instance.com/api/v1/repos/username/repo/hooks' \
  -H 'Authorization: token YOUR_ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '{
  "type": "gogs",
  "config": {
    "url": "http://example.com/webhook",
    "content_type": "json",
    "secret": "your-webhook-secret"
  },
  "events": ["push", "issues"],
  "active": true
}'
```

Replace `YOUR_ACCESS_TOKEN`, `username`, `repo`, and other values as appropriate.

## Managing Webhooks

You can edit or delete existing webhooks from the same "Webhooks" section in your repository settings. For each webhook, you can:

- View recent deliveries and their responses
- Redeliver payloads
- Test the webhook with a ping event
- Edit the webhook configuration
- Delete the webhook

## Best Practices

1. Use HTTPS for your webhook URL to ensure the payload is encrypted.
2. Set a secret for your webhook to verify that the payload came from Gogs.
3. Ensure your server can handle the webhook payload quickly to avoid timeouts.
4. Monitor your webhook deliveries and handle any errors promptly.

## Troubleshooting

If you're having issues with your webhook:

1. Check the recent deliveries in the webhook settings to see if there are any errors.
2. Verify that your server is accessible and responding correctly.
3. Ensure that your server can handle the payload within the timeout period (usually 30 seconds).
4. Check that the events you've configured are the ones you expect to receive.

For more detailed information about the API and webhook payloads, refer to the [Gogs API documentation](https://github.com/gogs/docs-api).