# Laravel API Boilerplate

- Language: PHP 8.4
- Framework: Laravel 12
- Database: PostgreSQL 16, SQLite 3 (tests only)

## Goodies
- [Larastan](https://github.com/larastan/larastan) passing on the highest level available (10);
- [Sanctum](https://laravel.com/docs/12.x/sanctum) for Authentication;
  - Using UUIDs for the PersonalAccessTokens and for the Authenticable models;
  - Custom routes for authentication;
  - Tokens expire in [one year](config/sanctum.php);
- [Rollbar](https://docs.rollbar.com/docs/laravel) integration for error tracking
- [Swagger](https://swagger.io) (OpenAPI 3.1) for API documentation
  - The documentation is available on the `api.` subdomain of your application;
  - The documentation is disabled when the application is running in production (see `routes/api.php`);
  - Keep the documentation up-to-date on `resources\api\documentation.yaml`
- [Github Actions Workflow](.github/workflows/integration.yml) to ensure the new code is linted, tested and [larastan](https://github.com/larastan/larastan)-ed before merging into a root branch;
  - Make sure you enable branch protection on your repository (pull request before merging, approvals, up-to-date branches, conversation resolution) and require the following status checks to pass before merging: `lint`, `test` and `static-analysis`;
- [Laravel Translatable](https://github.com/spatie/laravel-translatable) for multi-language support;
- [Laravel Translations Loader](https://github.com/spatie/laravel-translation-loader) helps you provide translations from the database to your application using the API;
- [Laravel-Lang](https://github.com/Laravel-Lang/common) to manage your laravel translations. Check [the documentation](https://laravel-lang.com/introduction.html) on how to add languages or update existing;
- [PHP CS Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer) configuration file for code styling (PhpCsFixer rule-set with minor customizations);
- [Clockwork](https://github.com/itsgoingd/clockwork) gives you an insight into your application runtime - including request data, performance metrics, log entries, database queries, cache queries, redis commands, dispatched events, queued jobs, rendered views and more - for HTTP requests, commands, queue jobs and tests;
- [Secure Headers](https://github.com/bepsvpt/secure-headers) for adding security related headers to HTTP response. The following configs were changed from default: `x-frame-options`, `connect-src`, `default-src`, `font-src`, `img-src`, `script-src` (`self`, `unsafe-inline` and `unsafe-eval`), `style-src`
  - ⚠️ Once you set up SSL/TLS, remember to enable `hsts`;
- [Flysystem AWS S3 Adapter](https://github.com/thephpleague/flysystem-aws-s3-v3) is a sub-split of Flysystem library that provides an iteraction interface with AWS S3.
- [Slack Notifications](https://laravel.com/docs/12.x/notifications#slack-notifications) for sending notifications via Slack;
- Several endpoints that will help you quickly bootstrap your application. See `routes/api.php`;
- Route groups are attached to application subdomains (see `bootstrap/app.php`);
- [Prevents Lazy Loading](https://laravel.com/docs/12.x/eloquent-relationships#preventing-lazy-loading) helps you prevent shipping code that does not perform well;
- [Login Throttling](app/Http/Middleware/ThrottleLogin.php) based on [Laravel UI](https://github.com/laravel/ui/blob/master/auth-backend/ThrottlesLogins.php);
- [Application Localization](app/Http/Middleware/Localize.php) based on user preferences and `Accept-Language` header;
- [Custom error handling](bootstrap/app.php) to have standardized errors returned on the API endpoints;
  -  `message` is a localized field that can be displayed to the user;
  -  `error` is a more meaningful message for the developers;
- [Queue](https://laravel.com/docs/12.x/queues) setup to use the database driver;
- [Emails](https://laravel.com/docs/12.x/mail) already set up for email verification and password reset. It will take into account the [user preferred language](https://laravel.com/docs/12.x/mail#user-preferred-locales) when sending the email;
- [Pull-request template](.github/pull_request_template.md) so you don't forget about important things when merging code;
- [Automated Tests](tests/) for some methods and all endpoints. See the [Laravel Documentation on tests](https://laravel.com/docs/12.x/testing) to understand how they are split between Unit and Feature tests;

## Getting started


### Existing environment
Make sure you have PHP and PostgreSQL installed and running locally. Rename `.env.example.local` to `.env` and change the default values. You're good to go! For running tests make sure you have SQLite available.

```sh
$ git clone https://github.com/appname/boilerplate-api-laravel
$ cd boilerplate-api-laravel
$ composer install
$ cp .env.example.local .env
$ cp .env.example.test .env.test
# Edit .env files...
$ php artisan key:generate
$ php artisan migrate:fresh --seed
$ php artisan serve
# API docs at http://api.localhost:8000
```
