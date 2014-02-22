cd ~/Documents/workspace/customer_onboarding
daemon-kit -i cron demo_daemon

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step Zero

git checkout 94bd2135aeebd37a2ec83d88ad4c7d6d1b75dea7

Show off the table structure, compare to rails.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step One

git checkout ff319e43200c09cb001df921614d6124e9e3dd9f

Gemfile

Adding the sqlite3 gem

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step Two

git checkout 401a49f1dc0a0939d990db87c540b0fc7bc64ba0

Gemfile

Locking rufus. The examples that daemon-kit gives you are all specific to Rufus 2.x and since we're going to follow those examples I want to lock to that version of rufus. 

ALternatively you could probably using 3.x and write your code to work with that. But I haven't played with that option.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Step Three

git checkout e81cc9769eb64fda29123ba4624ff5aed41d876b

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

git checkout 8664eb46438cec7dda957459db15bf57fb6af17d

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

git checkout e8bd567fe81b0e580bf78b417527cce9b67cb491

libexec/customer_onboarding-daemon.rb

Kill daemon
DAEMON_ENV=development nohup ./bin/customer_onboarding &
tail -f log/development.log


