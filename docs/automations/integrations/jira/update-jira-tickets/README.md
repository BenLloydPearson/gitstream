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
