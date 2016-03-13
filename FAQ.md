# Introduction #

I have received some emails regarding the design decisions of django-cron and I thought I would make them public for all to ... **ahem** enjoy =D


## Original Message ##

BTW I have a technical question here: Why the cron has to be so sophisticated? I have written a very simple one. Could you please have a quick look and tell me why it is a bad idea? many thanks!

```
from threading import Timer
import time

t = 10

def cronjob():
    def job():       
             
        # do something

    job()
    Timer(t, cronjob).start()

cronjob()
```

## Response ##

  1. The Job in your code sample will **only run once**.
> > You need some code to restart the timer each time the job finishes.
  1. The code for your job is **obvlivious to other instances of the server**.
> > For example, if you set `ServerLimit` to 5 in apache, your job will run 5 times as often as you had specified in your variable 't'.
> > This could lead to race conditions and all sorts of other issues.
  1. When you restart the server, the cron jobs will not **be able to tell the last time they were run**.
> > So if you set `MaxRequestsPerChild` to something small like 3. It is very possible that your cron jobs intended to run once per day will be running far more often than that.
  1. Finally, I am a contributor to the `django-cron` project, but I did not write the original application, so there are some design decisions that I inherited :)