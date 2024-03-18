# Automatically Update Jira Tickets from PRs

Automatically update Jira tickets based on PR status.

[start:example]

!!! info "Conditions (All Must be True):"
    * The PR contains a reference to a Jira ticket in the title or description

!!! example "Automation Actions:"
    * Send an HTTP request to a Jira endpoint that updates the ticket status.

```yaml
update_jira:
    if:
      - {{ has.ticket_in_title or has.ticket_in_branch }}
    run:
      - action: send-http-request@v1
        args:
          url: "https://automation.atlassian.com/pro/hooks/__AUTOMATION_WEBHOOK_URL__"
          method: POST
          headers: '{"Content-type": "application/json"}'
          body: '{"issues":["{{ticketid}}"]}'
```

![Automation Example](./update-jira.png)

[end:example]
