---
title: Apprise
tags: [automation]
---
Ever wanted to broadcast a single notification over Matrix, ntfy, PagerDuty, and AWS SES? That's what [Apprise](https://github.com/caronc/apprise/) is good for.
Here's the initial `docker-compose.yml` I used to try it out:
```docker title="docker-compose.yml"
services:
  apprise:
    image: caronc/apprise:latest
    container_name: apprise
    restart: always
    ports:
      - 8000:8000
    volumes:
      - /var/lib/apprise/config:/config
```
---
Accessing APPRISE_IP:8000 presents a dashboard. In the sidebar, choose "New Configuration" to create a new endpoint that is capable of broadcasting to the services mentioned above.
## Apprise Syntax
There's syntax for adding each service, luckily they're well documented in the [apprise/wiki](https://github.com/caronc/apprise/wiki) and on the "Apprise Details" page within the dashboard.

### Examples
```
pagerduty://{integration_key}@{api_key}
ntfy://{token}@{hostname}/{targets}
discord://{botname}@{WebhookID}/{WebhookToken}/
```

## Usage
Once the endpoint is configured, there are instructions for using it on the "Overview" tab in the Apprise web interface:
```
curl -X POST \  
    -F "body=Test Message" \  
    -F "tags=all" \  
    https://apprise.mydomain.com/notify/xyWOOAt2vHscUJ4kh0nTOdR39aI3g/Wm0p8LODPipnrVMajdwUzCi3H36nINXy3f
```

We'd expect a notification to be broadcast using every service configured.