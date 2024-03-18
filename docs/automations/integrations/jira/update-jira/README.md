# Automatically Update Jira Tickets from PRs

[start:example]

!!! info "Automatically update Jira tickets based on PR status"
    **Conditions (All Must be True):**
    - The PR contains a reference to a Jira ticket in the title or description

    **Automation Actions**
    - Send an HTTP request to a Jira endpoint that updates the ticket status.

!!! example "Configuration"
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

![Placeholder for image](./image.png)

[end:example]
