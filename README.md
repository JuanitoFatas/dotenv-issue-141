README
======

[config/application.rb#L9](https://github.com/JuanitoFatas/dotenv-issue-141/blob/master/config/application.rb#L9):

```
abort('ENV NOT FOUND') if ENV['HOSTNAME'].blank?
```

With dotenv-rails 1.0.1 & 1.0.1
-------------------------------

run `rails console` you should see ENV NOT FOUND.

With dotenv-rails < 1.0
-----------------------

it works.

My case
-------

So in my real app I was trying to set the `default_url_options` like this:

```
require File.expand_path('../boot', __FILE__)

require 'rails/all'

# Require the gems listed in Gemfile, including any gems
# you've limited to :test, :development, or :production.
Bundler.require(*Rails.groups)

HOSTNAME = ENV['HOSTNAME']

module Dotenv
  class Application < Rails::Application
    config.action_mailer.default_url_options = { host: HOSTNAME }
  end
end
```

My workaround is to load it by myself:

```
Dotenv.load if Rails.env.development? || Rails.env.test?
```

Thank you in advance.
