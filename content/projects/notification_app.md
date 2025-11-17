---
title: "Notification App"
date: 2025-10-27
description: "Python-based app that sends local weather forecasts via email using OpenWeather API and Gmail SMTP."
tldr: "Automated weather alert system using Python, OpenWeather, cron, and custom logging."
repo: "https://github.com/rmitchell745/weather-app"
mermaid: true
milestones:
  - Established OpenWeather API integration
  - Send Email to MMS for multiple users
  - Deploy on Server and schedule via Cron 
  - adjust timezones for each user, update code to only send at times specified in user configuration
  - Refactor to send MMS directly
  - Dockerize, Deploy, and schedule with systemd 
  - establish ML learning model using public data to predict traffic travel time. 
---

### Overview
The **Weather Notification App** is a Python-based automation tool that retrieves upcoming forecasts and sends scheduled email alerts. It runs on your local server via cron jobs and uses a lightweight configuration file for flexible scheduling and city selection.

### Current Key Features
- Pulls forecasts from OpenWeather’s 3-hour endpoint  
- Custom logging system for local and Docker environments  
- Scheduled via cron, compatible with containerized deployments  
- Sends daily emails with concise weather summaries  

{{< mermaid >}}
graph TD;
    A[OpenWeather API] --> B[Weather Script]
    E --> C[Logger]
    E --> D[Email Sender]
    B --> E[Main Script]
{{</ mermaid >}}





