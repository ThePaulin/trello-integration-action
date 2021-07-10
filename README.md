# Trello integration action

The action looks for Trello card URL within the Pull Request description and comments. If found, it will add the Pull Request URL as an attachment to the Trello card. When PR is opened or closed, it will move the card to a defined list.

```yaml
name: Trello integration
on:
    pull_request:
        types: [opened, edited, closed]
    issue_comment:
        types: [created, edited]
jobs:
    build:
        runs-on: ubuntu-latest
        steps:
            - uses: rematocorp/trello-integration-action@main
              with:
                  github-token: ${{ secrets.GITHUB_TOKEN }}
                  trello-api-key: ${{ secrets.TRELLO_API_KEY }} # https://trello.com/app-key
                  trello-auth-token: ${{ secrets.TRELLO_AUTH_TOKEN }} # https://trello.com/app-key then click generate a token
                  trello-list-name-pr-open: ${{ secrets.TRELLO_PR_OPEN_LIST_ID }} # Trello list ID for open pull request, visit a board then append .json to url to find id
                  trello-list-name-pr-closed: ${{ secrets.TRELLO_PR_CLOSED_LIST_ID }} # Trello list ID for closed pull request, visit a board then append .json to url to find id
```

Inspired by [dalezak/github-commit-to-trello-card](https://github.com/dalezak/github-commit-to-trello-card) and [delivered/attach-to-trello-card-action](https://github.com/delivered/attach-to-trello-card-action).
