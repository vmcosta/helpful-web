# Supportly

[![Build Status](https://travis-ci.org/support-foo/web.png?branch=master)](https://travis-ci.org/support-foo/web)

## Support that makes you better at support.

This is a placeholder repo for a product that's under review at Assembly. You can help this idea get made into a product by visiting [https://assemblymade.com/support-foo](https://assemblymade.com/support-foo).

### Proposed Stack

  * Web app, written in Ruby on Rails, hosted on Heroku
  * Mac desktop app, written in Objective-C
  * Windows desktop app, written in C#

### How Assembly Works

Assembly products are like open-source and made with contributions from the community. Assembly handles the boring stuff like hosting, support, financing, legal, etc. Once the product launches we collect the revenue and split the profits amongst the contributors.

Visit [https://assemblymade.com](https://assemblymade.com) to learn more.

## Getting started with development

*Note: This assumes you have Ruby 1.9.2 or later installed properly and have a basic working knowledge of how to use RubyGems*

First you'll need to fork and clone this repo.

```
git clone git://github.com/support-foo/web.git web
cd web
```

Let get our dependencies setup:

```
bundle install --path .bundle --binstubs
```

Now let's get some configuration in place

```
cp config/database.yml.example config/database.yml
cp .env.example .env
```

Now let's create the databases

```
bundle exec rake db:setup
```

Now run this thing!

```
bundle exec foreman start
```

Everything should be up and running here [http://0.0.0.0:5000](http://0.0.0.0:5000)

### Background working (with Sidekiq)

As proposed Sidekiq is used for background working.

Put "jobs" in app/workers directory (Resque syntax is supported).

Sidekiq needs a Redis server, recommended are RedisToGo (available for free at Heroku).

Before launcing in production sidekiq should be tuned acording to numbers of web (workers) in use.

[http://manuel.manuelles.nl/sidekiq-heroku-redis-calc](http://manuel.manuelles.nl/sidekiq-heroku-redis-calc) gives some nice estimations for numbers to use.

Number of concurrent workers can be set by env. variable ```SIDEKIQ_CONCURRENCY``` and updating ```config/initializers/sidekiq.rb```

Sidekiq admin view (/sidekiq) is available in _development_ environment only.

