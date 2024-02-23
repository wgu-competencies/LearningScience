name: PR Failure Notification
on:
    pull_request:
        types: [closed]

jobs:
  notifyTeamsOnFailure:
    runs-on: ubuntu-latest
    if: ${{ github.event.pull_request.merged == false && github.event.pull_request.state == 'closed' }}
    steps:
    - name: Notify Teams
      uses: ravsamhq/notify-teams@v1
      with:
        webhook-url: ${{ secrets.TEAMS_WEBHOOK_URL }}
        message: "A pull request failed QA checks!"
