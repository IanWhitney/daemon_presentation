Before

I would create a cron-like daemon using this

daemon-kit -i cron customer_onboarding

Daemon Kit lets you create daemons of a few different styles. The major difference is that the cron-like ones work on a timed schedule and the others respond to messages or queuing systems. We'll go with cron-like here since it's a bit more straightforward to get going.

I generated this skeleton of this daemon earlier, so let's check it out and get it working.

cd ~/Documents/workspace/customer_onboarding

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step Zero

demo0

Show off the table structure, compare to rails.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step One

demo1

Gemfile

Adding the sqlite3 gem

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step Two

demo2

Gemfile

Locking rufus. The examples that daemon-kit gives you are all specific to Rufus 2.x and since we're going to follow those examples I want to lock to that version of rufus. 

ALternatively you could probably using 3.x and write your code to work with that. But I haven't played with that option.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step Three

demo3

libexec/customer_onboarding-daemon.rb

The rake task is where the real work is done. You want the code in
libexec/customer_onboarding-daemon.rb to be as light as possible, since
it's what will be growing (or not) the memory footprint of your daemon.

Calling rake is perfect because it will run in a separate process and
that process will die once the work is complete. So you don't have to
worry about that memory.

Mention Jim Weirich toast after meeting

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step Four

demo4

tasks/onboarding.rake

Write the rake task that you're calling from
libexec/customer_onboarding-daemon.rb.

Since this is a demonstration, this task doesn't actually do anything.
Real work is left as an exercise for the reader.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step Five

cd ~/Documents/workspace/customer_onboarding
./bin/customer_onboarding

And....nothing happens! This is exactly what should happen, as the rake task is being called in a rake task and not in our daemon. But it is running. Look.

ps aux | grep rake

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step Six

demo5

libexec/customer_onboarding-daemon.rb

Kill daemon
DAEMON_ENV=development nohup ./bin/customer_onboarding &
tail -f log/development.log


