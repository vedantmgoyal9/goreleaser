# Teams

To use [Teams](https://www.microsoft.com/de-de/microsoft-teams/group-chat-software), you need
to [create a Webhook](https://docs.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook)
, and set following environment variable on your pipeline:

- `TEAMS_WEBHOOK`

After this, you can add following section to your `.goreleaser.yaml` config:

```yaml title=".goreleaser.yaml"
announce:
  teams:
    # Whether its enabled or not.
    #
    # Templates: allowed (since v2.6).
    enabled: true

    # Title template to use while publishing.
    #
    # Default: '{{ .ProjectName }} {{ .Tag }} is out!'.
    # Templates: allowed.
    title_template: "GoReleaser {{ .Tag }} was just released!"

    # Message template to use while publishing.
    #
    # Default: '{{ .ProjectName }} {{ .Tag }} is out! Check it out at {{ .ReleaseURL }}'.
    # Templates: allowed.
    message_template: "Awesome project {{.Tag}} is out!"

    # Color code of the message. You have to use hexadecimal.
    #
    # Default: '#2D313E' (the grey-ish from GoReleaser).
    color: ""

    # URL to an image to use as the icon for the message.
    #
    # Default: 'https://goreleaser.com/static/avatar.png'.
    icon_url: ""
```

<!-- md:templates -->
