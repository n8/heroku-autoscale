# Heroku::Autoscale

    This is a fork of @ddollar's original gem. It's a bit quick and dirty right now. 
    
    The main change I wanted to make was to have the scaling action this performs to be explicit. So instead of having code invoked on every single web request that this gem intercepts (it's a Rack app) which doesn't work for anyone that has multiple dynos going in production, you now have to explicitly ask your app to auto scale using a GET request to the app. 
    
    With that in place, you can issue that GET request from cron or clockwork or some alternative so that you don't have to worry about your autoscale commands running concurently. 

## Installation

    # Gemfile
    gem 'heroku-autoscale', :git => "git@github.com:n8/heroku-autoscale.git"

## Usage (Rails 2.x)

    # config/environment.rb
    use Heroku::Autoscale,
      :username  => ENV["HEROKU_USERNAME"],
      :password  => ENV["HEROKU_PASSWORD"],
      :app_name  => ENV["HEROKU_APP_NAME"],
    	:autoscale_key => ENV["HEROKU_SCALE_KEY"],
      :min_dynos => 5,
      :max_dynos => 30,
      :queue_wait_low  => 100,  # milliseconds
      :queue_wait_high => 1000, # milliseconds
      :min_frequency   => 10    # seconds
    
## Usage (Rails 3 / Rack)

    # config.ru
    use Heroku::Autoscale,
      :username  => ENV["HEROKU_USERNAME"],
      :password  => ENV["HEROKU_PASSWORD"],
      :app_name  => ENV["HEROKU_APP_NAME"],
    	:autoscale_key => ENV["HEROKU_SCALE_KEY"],
      :min_dynos => 5,
      :max_dynos => 30,
      :queue_wait_low  => 100,  # milliseconds
      :queue_wait_high => 1000, # milliseconds
      :min_frequency   => 10    # seconds