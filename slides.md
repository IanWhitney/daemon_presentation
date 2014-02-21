# Daemons in Ruby
## Or, how I learned to 


# First and Foremost


### D[a]emons?

Note: Discussing this is about as useful as vim/emacs, and half as fun.

### Definiton

A stand-alone process that runs in the background that perorms a small number of tasks

### Solutions For:

Any task that
- doesn't have to happen instantly, or...
- takes a long time, or...
- needs to be constantly on the alert

Note:
Examples:
  - Confirmation emails, 
  - Data transformation, reports
  - Event-triggered scripts that need to run faster than cron


### You've probably already used them

Resque and Delayed Job use daemons under the hood.

Note: 
Sidekiq is not process-based. It uses threads.


### Great, I'll just use Resque or DJ


That's [mostly] fine.


### Why should I do more work?


You want more flexibility
Note:
My experience is with DJ and I've found it pretty fussy if I want to do anything interesting. Maybe Resque is better. And DJ is probably improving, as it has an enthusiastic and smart new maintainer, Erik Michaels-Ober from SoundClound. That aside, as vital as gems are, I always run into something that I want them to do that the can't/won't. These are no different.



You want more memory
Note:
Resque and DJ work by serializing objects from your app. To de-serialize them, they need to know about your app's objects. As a result they have all of rails. A totally unscientific observation, daemons I've had DJ create take about 2% of my server's memory than daemons I've spun up outside of Rails.



You're not dead inside
Note:
If your job is like mine, most of your life is in the MVC universe. Writing a daemon is a refreshing break.


### Goddamn, let's build a daemon!


Great. First, how are you going to handle PID management?
Note:
Can't skip this. Without PID management you can't easily kill the process or see what's running.



Oh, and logging.
Note:
Everyone loves logging. Gotta log em all.



Don't forget about errors.
Note:
Though I'm sure your code will never fail, someone else could break your daemon and you'll want to know how.



### My enthusiasm has wained
Note:
This is the plumbing of every daemon, and it's interesting to do this yourself. But we'll skip it for now. If you want to know more, there's a good post by Jessie Stormer that I'll link to in my show notes on GitHub.


### Skip to the good stuff



How much would you pay for PID managament?



What if I throw in logging for free?



And, just for the next 2 hours, error capturing. Totally free!


## Daemon Kit
Daemons! You know, for kids!
Note: 
The simplest pitch for DK is that it's Rails for Dameons. It has generators that handle the repetitive plumbing and you just write your business logic.


## My enthusiasm has returned!


[live demo]
- Code up a quick daemon. It should look at a sqlite db for new entries in a customer table.
  when it sees them, it does an "onboarding" task. 
  It should run every 5 seconds.

- Ready to go before hand
  - Customer sign-up site
  - DB.yml file for the cron

- Create cron daemon
- Build rake task
- Testing
- Hook into libexec
- Run


## Deployment and Management

