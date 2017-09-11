# What is this?
This is basic api-only rails app used (in my case) as the backend for an ember application. This repo goes hand-in-hand with [this repo for an Ember base application](https://github.com/BaasNiel/ember-base). I use these repos to get an app up-and-running in a few minutes. You can copy the repos or follow the steps below to get up-and-running quickly.

# Steps
1. `rails new app-name -d postgresql --api`
2. Add cors and AMS to Gemfile and `bundle install`
    ```
    gem 'rack-cors'
    gem 'active_model_serializers', '~> 0.10.0'
    ```
3. `rails db:create`
    * Specify database names in `config/database.yml` if you need specific db names
4. Add `gem "pry-byebug"` in Gemfile **under development group** for debugging with `binding.pry`
5. Modify cors initializer (`config/initializers/cors.rb`) to include:
    ```
    Rails.application.config.middleware.insert_before 0, Rack::Cors do
        allow do
            origins '*'

            resource '*',
            headers: :any,
            methods: [:get, :post, :put, :patch, :delete, :options, :head]
        end
    end
    ```
    * **Note** that this will allow requests from anywhere. You may want to restrict this to only allow               requests from your own app.
6. Modify `config/application.rb` to include:
    ```
    ActiveModel::Serializer.config.adapter = :json
    ActiveModel::Serializer.config.key_transform = :camel_lower
    ```

Your api is ready. You can now go set up a model with a controller and serializer. Try `rails generate scaffold model`to generate some files for you to get started.

# Useful Resources
1. https://spin.atomicobject.com/2017/03/06/rails-ember-cli/
2. https://wyeworks.com/blog/2015/6/30/how-to-build-a-rails-5-api-only-and-ember-application
