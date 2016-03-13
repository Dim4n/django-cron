The django app will allow the site to run code in a cron job like manor without needing to setup a real cron job (Useful for people hosting on windows or with Hosting companies that do not give you access to setup cron jobs).

To create a Cron Job you create a file called cron.py in your application directory that will contain the jobs you wish to run. Once you have your jobs created you need add two lines to your primary urls.py (Similar to what you need to do for the admin site)
```
import django_cron
django_cron.autodiscover()
```
That will go though all your installed apps and see if they have a cron job to register

## Example Cron Job included in the application ##
```
from django_cron import cronScheduler, Job

# This is a function I wrote to check a feedback email address and add it to our database. Replace with your own imports
from MyMailFunctions import check_feedback_mailbox

class CheckMail(Job):
	"""
		Cron Job that checks the lgr users mailbox and adds any approved senders' attachments to the db
	"""

	# run every 300 seconds (5 minutes)
	run_every = 300
		
	def job(self):
		# This will be executed every 5 minutes
		check_feedback_mailbox()

cronScheduler.register(CheckMail)
```