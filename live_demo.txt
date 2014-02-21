cd ~/Documents/workspace/
daemon-kit -i cron demo_daemon
cd demo_daemon
# add sqlite3 to Gemfile

bundle install

# open up libexec/demo_daemon-daemon
# create rake task that calls onboard:customers


    DaemonKit::Cron.scheduler.every("5s") do
      `bundle exec rake -f '#{DAEMON_ROOT}/tasks/onboard.rake' onboard:customers`
    end

# talk a little about the importance of keeping this light
# create the rake file
# Mention Jim Weirich toast after meeting

touch tasks/onboard.rake

# Write the task.

    namespace :onboard do
      task :customers do
        require 'sqlite3'
        db = SQLite3::Database.new "/Users/Ian/Documents/workspace/daemon_presentation/customer_signup/db/development.sqlite3"
        db.execute("select * from users") do |user|
          sleep(4)
          puts user.inspect
        end
      end
    end

./bin/demo_daemon

# And....nothing happens! This is exactly what should happen, as the rake task is being called in a rake task and not in our daemon. But it is running. Look.

ps aux | grep rake 

# edit the cron task in libexec/demo_daemon-daemon

    DaemonKit::Cron.scheduler.every("5s") do
      `bundle exec rake -f '#{DAEMON_ROOT}/tasks/onboard.rake' onboard:customers`
      DaemonKit.logger.error "You done busted it"
    end

# re-run the daemon and tail the /log/development.log file
