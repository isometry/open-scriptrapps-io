# vRealize Operations Manager to Slack notification bridge

A simple serverless bridge enabling realtime push of vRealize Operations Manager REST notifications to a Slack channel of your choice.

## Usage

 - Configure a [Slack Custom Integration](https://api.slack.com/custom-integrations) associated with the channel in which you want to receive notifications. Note the 'secret' part of the WebHook URI, referred to here as the parameter `webhook` (e.g. https://hooks.slack.com/services/<em>T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX</em>).

 - Test the custom integration via curl(1) at the command line:

```
curl -X POST 'https://open.scriptrapps.io/v1.0/vrops/slack/notification?webhook=T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX'
```

 - Configure vRealize Operations Manager REST Notifications Rule to use the REST Notification Plugin, configured with a target URL ofy] `https://open.scriptrapps.io/v1.0/vrops/slack/notification?webhook=T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX`, blank credentials, a Content type of `application/json` and a Certificate Thumbprint of `17:EF:95:BB:D0:7E:9A:43:E9:6C:A2:B6:4E:E2:E8:B4:21:3E:C9:CB` (correct as-of 2016-11-26).

## Appearance

Notifications are rendered to Slack in the following format:

> **Web service – Tier Health is degraded** (Status=ACTIVE Impact=health Health=2 Risk=1 Efficiency=1)

## Optional Configuration

### Enable rich messages with direct links back to vROps

By default, notifications will not be linked back to your vROps instance. By including an additional `host` parameter in the URL, both affected object and the alert will be rendered as deep links back to the associated items in your vROps instance:

`https://open.scriptrapps.io/v1.0/vrops/slack/notification?webhook=T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX&host=vrops.example.com`

### Customise the notification bot's name and icon

By default, the notification bot is called `vrops` and is represented by the [traffic_light](http://www.webpagefx.com/tools/emoji-cheat-sheet/#e_648) icon. To rename the bot or specify an alternative icon, include either or both of the `username` and `icon` parameters:

`https://open.scriptrapps.io/v1.0/vrops/slack/notification?webhook=T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX&username=Bob&icon=vrops`

### Post to an alternative channel

By default, notifications will go to whichever channel the Slack WebHook was created for. This can be overridden with the `channel` parameter:

`https://open.scriptrapps.io/v1.0/vrops/slack/notification?webhook=T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX&channel=#vrops`

Tip: public channels get the `#` prefix, private channels do not; messages can be sent to a single user by specifying `channel=@username`

Tip: create multiple REST Notification Plugin instances differentiated only by the `channel` parameter to send different notifications to different channels.
