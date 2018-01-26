# Daemons in Ruby
## Why and How
Ian Whitney (@IanWhitney)<br /> University of Minnesota



(or as much as is possible in 15 minutes)
Note:
Breadth of subject and purpose of talk.



# First and Foremost


## D[a]emons?
Note: Discussing this is about as useful as vim/emacs, and half as fun. Probably 'demons'. But everyone says 'daemon'. Let's move on.



## Definition


### A stand-alone process that runs in the background that perorms task[s].
Note: A one task-per-daemon rule is probably good. But I don't think the process police are going to bust you for breaking that rule.



## Solutions For:


### Any task that:
#### Doesn't have to happen instantly<!-- .element: class="fragment" data-fragment-index="1" -->
#### Takes a long time<!-- .element: class="fragment" data-fragment-index="2" -->
#### Does need to happen instantly<!-- .element: class="fragment" data-fragment-index="3" -->
Note: 
Confirmation emails
Data transformation
Event-trigged code that has to be faster than cron's 1-minute limit



## You've probably already used them
Note: Resque and Delayed Job use daemons under the hood. Sidekiq is not process-based. It uses threads.



## Problem solved!
### I'll just use Resque || DJ
Note: That's [mostly] fine.



# Why should I do more work?


## You want more:
### Flexibility<!-- .element: class="fragment" data-fragment-index="1" -->
### Memory<!-- .element: class="fragment" data-fragment-index="2" -->
### Fun<!-- .element: class="fragment" data-fragment-index="3" -->
Note:
My experience is with DJ and I've found it pretty fussy if I want to do anything interesting. Maybe Resque is better. And DJ is probably improving, as it has an enthusiastic and smart new maintainer, Erik Michaels-Ober from SoundClound. That aside, as vital as gems are, I always run into something that I want them to do that the can't/won't. These are no different.

Resque and DJ work by serializing objects from your app. To de-serialize them, they need to know about your app's objects. As a result they have all of rails. A totally unscientific observation, daemons I've had DJ create take about 2% of my server's memory than daemons I've spun up outside of Rails.

If your job is like mine, most of your life is in the MVC universe. Writing a daemon is a refreshing break.



# Goddamn!<br/>
## Let's build a daemon!


## The groundwork
### Logging<!-- .element: class="fragment" data-fragment-index="1" -->
### Errors<!-- .element: class="fragment" data-fragment-index="2" -->
### Scheduling<!-- .element: class="fragment" data-fragment-index="3" -->
Note:

Everyone loves logging. When did the daemon run, why did it run, what did it do, etc. Someone will want to know this.

Though I'm sure your code will never fail, someone else could break your daemon and you'll want to know how.

How will your daemon know that it has work to do? Cron? Event-based? Message queue?



# My enthusiasm has wained
Note:
Yeah, I feel you. This is the repetitive plumbing of every daemon. If only someone could make it go away...



# But Wait!


## How much would you pay for...


### Logging?
For the first 50 customers!


### Error Capturing?
Totally free. Call now!


### Scheduling?
Just pay shipping and handling!


# Daemon Kit
Note: 
The simplest pitch for DK is that it's Rails for Dameons. It has generators that handle the repetitive plumbing and you just write your tests and business logic.



## My enthusiasm has returned!
Note: Well, before I dissapoint you again, let's make that daemon.



## Questions?
- https://github.com/kennethkalmer/daemon-kit
- https://github.com/IanWhitney/daemon_presentation
- https://github.com/IanWhitney/customer_onboarding
