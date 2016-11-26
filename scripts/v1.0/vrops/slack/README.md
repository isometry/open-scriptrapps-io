# vRealize Operations Manager to Slack notification bridge

A simple serverless bridge enabling realtime push of vRealize Operations Manager notifications to a Slack channel of your choice.

## Usage

1. Configure a Slack WebHook associated with the channel in which you want to receive notifications. Note the webhook's secret part, referred to here as the parameter `webhook` (e.g. https://hooks.slack.com/services/<em>T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX</em>).
2. Configure vRealize Operations Manager REST Notifications Rule to use the REST Notification Plugin, with a target URL `https://open.scriptrapps.io/v1.0/vrops/slack/notification?webhook=T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX, and a Certificate Thumbprint of `17:EF:95:BB:D0:7E:9A:43:E9:6C:A2:B6:4E:E2:E8:B4:21:3E:C9:CB`.

## Optional Configuration

### Link back to vROps

By default notifications will not be linked back to your vROps instance. By including an additional `host` parameter in the URL, both affected object and the alert will be rendered as direct links back to your vROps instance:

`https://open.scriptrapps.io/v1.0/vrops/slack/notification?webhook=T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX&host=vrops.example.com`

### Change the Bot's name and icon

By default the notification bot is called `vrops` and is represented by the [traffic_light](http://www.webpagefx.com/tools/emoji-cheat-sheet/#e_648) icon. To rename the bot or specify an alternative icon, include either or both of the `username` and `icon` parameters:

`https://open.scriptrapps.io/v1.0/vrops/slack/notification?webhook=T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX&username=Bob&icon=vrops`

### Non-default channels

By default notifications will go to whichever channel the Slack WebHook was created for. This can be overridden with the `channel` parameter:

`https://open.scriptrapps.io/v1.0/vrops/slack/notification?webhook=T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX&channel=#vrops`
