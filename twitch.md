# Twitch Auto Announcements Using [IFTTT](https://ifttt.com/)
To setup automatic announcements for when a Twitch Streamer goes live, head over to [IFTTT](https://ifttt.com/create) and create a new applet. Click on this and select Twitch. Connect your Twitch Account if prompted. Click on that and select Webhooks.

Head over to Discord and create a new Webhook. Configure the settings as needed. After you're done, copy the Webhook URL and paste it in "Make a web request" on IFTTT. Also select whichever channel you want auto announcements for. Change the "Method" to `POST` and "Content Type" to `application/json`.

After all that's done, use the template below as the "Body." Remember to change `role_id` in `content` and `twitch_profile_picture_url` in `thumbnail.url` and `author.url`. This example uses all available ingredients except `CurrentViewers`.

```json
{
    "content": "<@&role_id>, {{ChannelName}} went live on Twitch",
    "allowed_mentions": {
        "parse": ["roles"]
    },
    "embeds": [{
        "title": "{{ChannelName}} went live on {{ChannelUrl}}",
        "url": "{{ChannelUrl}}",
        "color": 6570404,
        "footer": {
            "text": "{{CreatedAt}}"
        },
        "image": {
            "url": "{{StreamPreview}}"
        },
        "thumbnail": {
            "url": "twitch_profile_picture_url"
        },
        "author": {
            "name": "{{ChannelName}} is now streaming",
            "url": "{{ChannelUrl}}",
            "icon_url": "twitch_profile_picture_url"
        },
        "fields": [{
            "name": "Playing",
            "value": "{{Game}}",
            "inline": true
        }, {
            "name": "Started at",
            "value": "{{CreatedAt}}",
            "inline": true
        }]
    }]
}
```
