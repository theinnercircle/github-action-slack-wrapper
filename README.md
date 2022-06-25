# github-action-slack-wrapper

Slack notification wrapper

## Usage examples

Without attachment

```yaml
steps:

- name: Slack notification
  uses: theinnercircle/github-action-slack-wrapper@v1
  with:
    channel: C03G974LSSX
    text: ${{ format('*{0}* pull request <{1}|{2}> deployed by _{3} ({4})_', github.event.repository.name, github.event.pull_request.html_url, github.event.pull_request.title, github.actor, needs.prepare.outputs.actor-name) }}
  env:
    SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}
```

With attachment

```yaml
steps:

- name: Slack notification
  uses: theinnercircle/github-action-slack-wrapper@v1
  with:
    channel: C03G974LSSX
    text: ${{ format('*{0}* branch `{1}` deployed to *{2}* by _{3} ({4})_', github.event.repository.name, github.event.repository.default_branch, needs.prepare.outputs.target, github.actor, needs.prepare.outputs.actor-name) }}
    attachment-text: ${{ format('<{0}|Trigger comment>, <{1}/commit/{2}|commit>', github.event.comment.html_url, github.event.repository.html_url, github.sha) }}
  env:
    SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}
```
