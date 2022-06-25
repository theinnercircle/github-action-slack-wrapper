# github-action-slack-wrapper

Slack notification wrapper

## Usage examples

Simplest use-case, default parameters and no attachment

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

Full example

```yaml
steps:

- name: Slack notification
  uses: theinnercircle/github-action-slack-wrapper@v1
  with:
    channel: C03G974LSSX
    username: github-actions
    icon-url: https://avatars.githubusercontent.com/in/15368?v=4
    text: ${{ format('*{0}* branch `{1}` deployed to *{2}* by _{3} ({4})_', github.event.repository.name, github.event.repository.default_branch, needs.prepare.outputs.target, github.actor, needs.prepare.outputs.actor-name) }}
    attachment-text: ${{ format('<{0}|Trigger comment>, <{1}/commit/{2}|commit>', github.event.comment.html_url, github.event.repository.html_url, github.sha) }}
  env:
    SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK }}
```
