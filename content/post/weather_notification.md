+++
title = "Building a Python Weather Notification App: Lessons in Automation, APIs, and DevOps"
date = 2025-10-28
description = "A look at how I built and automated a weather alert app that delivers daily forecasts via email-to-MMS using Python, YAML configs, and cron jobs."
tags = ["python", "automation", "devops", "weather-app", "api", "smtp"]
draft = false
+++


# Building a Python Weather Notification App: Lessons in Automation, APIs, and DevOps


## TL;DR
I built a **Python-based weather notification system** that pulls real-time forecasts from the **OpenWeather API**, formats them for readability, and delivers them as **MMS messages via Gmail SMTP**.  
The app runs automatically on the home server, scheduled with **cron**, and logs all activity. 


**Stack:** Python, OpenWeather API, YAML, smtplib (SSL), cron, Fedora Server  
[GitHub Repo](https://github.com/rmitchell745/notification_app.git)  


---


## Introduction
After setting up my homelab and blog, I wanted to build something practical that I could automate — something that combined Python, working with APIs, and easy to deploy as I move further into containerization and orchestration. The thought of a weather app and its next steps hit me while managing my morning routine and getting the kids ready for school, when my child asked, as they do everyday in the fall, is it going to be warmer or cold today? What type of jacket do I need to bring? I remembered back to when I was running all the time a simple app that I could plug in my current weather, the time of day, and the time I would run and it would give me an outfit recommendation. The current result is a lightweight notification app that texts me and my family the weather each morning before the commute.This app isn’t quite finished, I eventually want to add an outfit recommendation for the children, and include traffic projections and an ML model that can update the predictions based on the weather for the adults. 


This project helped reinforce my DevOps workflow habits — Git, automation, configuration through YAML, modular scripting, and logs for observability and trouble shooting.


---


## Architecture Overview


"""
[Config YAML] → [Weather Module] → [Email Module] → [Logger] → [Cron Job / Docker]
"""


**Core components:**
- **config.yml** – Stores user info (zip codes, phone numbers, carriers, email credentials).  
- **weather.py** – Pulls weather data from OpenWeather’s 5-day/3-hour forecast API.  
- **email_module.py** – Uses Gmail SMTP over SSL to send messages.  
- **logger.py** – Module for consistent log formatting and output.  
- **main.py** – Orchestrates all modules and runs as a cron job.  


---


## Hurdles and Debugging Lessons


### 1. Environment Variables and API Keys  


I established the API keys as persistent environment variable in .bashrc and everything ran fine in the test cases, but cron jobs don’t inherit shell environments the same way as interactive sessions, which I found out on the first auto run. 


**Fix:**
I sourced my .bashrc file in crontab to access the environment variables defined there to support automation.  I plan to use a ‘.env’  document as I move to containerization. 


“””
#add to the beginning of cron job in crontab


. $HOME/.bashrc;
“””


---


### 2. Relative and Absolute paths
I initially used relative paths to both the configuration file and the logger output, both of which were broken when the script was run in the cron environment. The fix to this was relatively easy, and was able to be done modularly using the “__file__”   variable in python with the OS module to return absolute paths to the file even if the project structure moves. 


“””
#from
cwd = os.getcwd() #returned a different directory when run by cron, or even when run outside the project root
config_path = os.path.join(cwd,"Config",'weather_config.yml')
#to
cwd = os.path.dirname(os.path.abspath(__file__))
config_path = os.path.join(cwd,"Config",'weather_config.yml')
“””
---


### 3. SMTP and SMS Gateways
Gmail’s SMTP server (`smtp.gmail.com`, port `465`) worked perfectly in my initial test case with a short “I love you message”  — but SMS messages truncate after ~160 characters depending on the carrier.  
Long messages with multiple zip codes were getting clipped or lost. I initially thought this was an issue in getting all the data from the API call, or in my code iterating over user zipcodes and generating messages. I spent more time than was necessary looking for an issue that wasn't there, putting debug log statements working my way up the chain ensuring that data wasn't lost until I confirmed the message that was sent to the sms gateway was correct. A quick google search later and I found verizon truncates their sms messages. 


It was a simple fix switch to the carrier’s mms gateway and the truncation issues were fixed. 


“””
#from 
"Verizon": "vtext.com",


#to
"Verizon": "vzwpix.com",


“””
---


## Example MMS Mesasge


“””
Hello Ryan,


Here is your weather forecast for the day:


Zipcode: 22202
Date: 2025-10-27
 - 03:00: Temp: 47.3°F | Clouds - broken clouds
 - 06:00: Temp: 47.1°F | Clouds - broken clouds
 - 09:00: Temp: 46.0°F | Clouds - broken clouds


Zipcode: 22315
Date: 2025-10-27
 - 03:00: Temp: 45.5°F | Clouds - broken clouds
 - 06:00: Temp: 45.3°F | Clouds - broken clouds
 - 09:00: Temp: 44.3°F | Clouds - broken clouds
“””


---


## Skills Practiced
- Python module design and structure  
- YAML configuration management  
- API integration and JSON parsing  
- Logging and debugging  
- Secure email transmission (SSL)  
- Cron automation and Linux job scheduling  
---

## Reflection
This project forced me to think about maintainability and automation, not just code execution.  
Every time the app failed silently or logged nothing, I needed to tighten my approach and gain more awareness of how Python interacts with the OS environment.

---

## Future Steps 
- Host the app on the homelab with **Mail-in-a-Box** integration in a Virtual Server  
- Store configs externally to support multi-user customization and container deployment
- Integrate **traffic data** into forecasts  
- build and implement ML model for accurate traffic forecast based on weather and news


---


## Resources
- [OpenWeather API Docs](https://openweathermap.org/forecast5) 
- [Python smtplib Docs](https://docs.python.org/3/library/smtplib.html)
- [Python Logging Tutorial](https://docs.python.org/3/howto/logging.html#logging-basic-tutorial)
- [Arch Linux Forums]()
- [Cron Environment Variables - stack overflow discussion](https://stackoverflow.com/questions/2229825/where-can-i-set-environment-variables-that-crontab-will-use)
