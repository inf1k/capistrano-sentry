# Capistrano::Sentry

Simple extension of capistrano for automatic notification of Sentry.

TODO: Prevent user at deployment start if missing parameter to inform sentry
      properly

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'capistrano-sentry'
```

Then, add this line to your application's Capfile:

```ruby
require 'capistrano/sentry'
```

And then execute from your command line:

```bash
bundle
```

## Usage

Add these lines to your application's `config/deploy.rb`:

```ruby
# Sentry deployment notification
set :sentry_host, 'https://my-sentry.mycorp.com' # https://sentry.io by default
set :sentry_api_token, '0123456789abcdef0123456789abcdef'
set :sentry_organization, 'my-org' # fetch(:application) by default
set :sentry_project, 'my-proj'     # fetch(:application) by default
set :sentry_repo, 'my-org/my-proj' # computed from repo_url by default

after 'deploy:published', 'sentry:notice_deployment'
```

* `sentry_host`: identifies to which host Sentry submissions are sent. [https://sentry.io by default]

* `sentry_api_token`: Deploy Tokens are project-specific and can be found on Sentry's Project Release Tracking
 page (`Project Settings > SDK Setup > Releases > Deploy Token`).
 [https://sentry.io/settings/{ORGANIZATION_SLUG}/projects/{PROJECT_SLUG}/release-tracking/]

* `sentry_organization`: The "**Name**" ("*A unique ID used to identify this organization*") from Sentry's Organization Settings page.
[https://sentry.io/settings/{ORGANIZATION_SLUG}]

* `sentry_project`: The "**Name**" ("*A unique ID used to identify this project*") from Sentry's Project Settings page.
[https://sentry.io/settings/{ORGANIZATION_SLUG}/projects/{PROJECT_SLUG}]

* `sentry_repo`: The `repository` name to be used when reporting repository details to Sentry [computed from `fetch(:repo_url)` by default -- `https://github.com/codeur/capistrano-sentry` becomes `//github.com/codeur/capistrano-sentry` and `git@github.com:codeur/capistrano-sentry.git` becomes `codeur/capistrano-sentry`]

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake test` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/codeur/capistrano-sentry. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the Capistrano::Sentry project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/codeur/capistrano-sentry/blob/master/CODE_OF_CONDUCT.md).
