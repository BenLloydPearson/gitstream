# -*- mode: yaml -*-

manifest:
  version: 1.0

provider: jira

orgName: #your Jira organization name here

assigneeRegex: r/(?<=\/gitstream assign-jira ).*(?=<br \/>)/

{% set ticketid = "" %}
{% for ticket in tickets %}
{% if (ticket | includes(regex=r/.+/)) %}
{% set ticketid = ticket %}
{% endif %}
{% endfor %}

automations:
  assign_jira:
    if:
      - {{ pr.description | includes(regex=assigneeRegex) }}
    run:
      - action: send-http-request@v1
        args:
          url: "https://automation.atlassian.com/pro/hooks/4792097928cdf034a7d23fc50e198068ba19fb41"
          method: POST
          headers: '{"Content-type": "application/json"}'
          body: '{"issues":["{{ticketid}}"],"data":{"assignee":"{{pr.description | capture(regex=assigneeRegex)}}"}}'
