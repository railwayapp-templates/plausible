# Railway: Plausible Analytics Template

[![Deploy on Railway](https://railway.app/button.svg)](https://railway.app/template/mzYEXO?referralCode=IFlm92)

## What is this template?

Plausible Analytics is a simple, open-source, lightweight (< 1 KB) and privacy-friendly alternative to Google Analytics. Plausible is trusted by 10,000+ paying subscribers to deliver their website and business insights.

This template makes it trivial to deploy an instance of [Plausible Analytics](https://plausible.io/) with all of it's required services on [Railway](https://railway.app).

See [the Plausible Analytics docsite](https://plausible.io/docs) for a more in-depth explanation of its feature set.

## Quick start guide

1. Click the "Deploy on Railway" button above, or [click here](https://railway.app/template/mzYEXO?referralCode=IFlm92)
2. Follow the setup steps in Railway
   - For information on the "optional" variables in the template, [see "Optional Variables" below](#optional-variables).
3. Monitor your services as they come up; wait until they're all up. 
4. Setup your websites with Plausible Analytics.
   1. Navigate to the domain for your Plausible Analytics service.
   2. Follow the prompts to create an account on the service
   3. Follow the prompts to set up tracking on your website.
   4. For more information on how to use Plausible, [check their site](https://plausible.io/docs).

## Optional variables

There are several "optional" environment variables for this template. This variables aren't needed to get Plausible Analytics running on Railway, but they add some niceties.

- **SMTP Mailer Setup**: these optional values enable your Plausible Analytics instance to send you emails. These can be weekly updates, or timely notifications if your site is getting a spike in traffic. [You can read more about these settings on Plausible Analytics docsite here.](https://plausible.io/docs/self-hosting-configuration#mailersmtp-setup)
  - `MAILER_EMAIL`: This is the email that all outgoing emails will come from (i.e. analytics@yoursite.com)
  - `MAILER_NAME`: This is the name that all outgoing emails will come from (i.e. Plausible Analytics for YourSite.com)
  - `SMTP_HOST_ADDR`: The host address of the SMTP server you'd like Plausible Analytics to use to send emails (i.e. send.mailserver.com)
  - `SMTP_HOST_PORT`: The port you'd like to use with `SMTP_HOST_ADDR` to send emails (i.e. 25, 225)
  - `SMTP_USER_NAME`: If your SMTP server of choice uses authentication, put the username here (i.e. smtp_user, admin@send.mailserver.com)
  - `SMTP_USER_PWD`: If your SMTP server of choice uses authentication, put the password here
  - `SMTP_HOST_SSL_ENABLED`: If your SMTP server support TLS encrypted traffic, enable it here (i.e true, false)

## Project structure & services

This template is made up of three "services":

- [Plausible Analytics](https://plausible.io/): the primary application.
  - The Plausible Analytics service is what you'll primarily be interacting with as a user. The service exposes a web application that users log in to, view analytics on, setup new sites with, change settings in, etc.
  - Plausible Analytics is run via [a Docker image the Plausible Analytics team publishes to DockerHub](https://hub.docker.com/r/plausible/analytics). Railway makes deploying images from DockerHub [very easy](https://docs.railway.app/develop/services#docker-image).
- [ClickHouse Database](https://clickhouse.com/): the analytics database.
  - ClickHouse is used to store Analytics data for Plausible Analytics. ClickHouse's architecture makes analytics data more efficient to query than PostgreSQL does, especially as data scales. This is likely why Plausible Analytics uses it for Analytics data. ([PostHog has a great article on this if you're interested in learning more.](https://posthog.com/blog/clickhouse-vs-postgres))
  - ClickHouse is run via [a custom dockerfile](https://github.com/railwayapp-templates/plausible/blob/main/packages/clickhouse/dockerfile.clickhouse), some [custom ClickHouse config](https://github.com/railwayapp-templates/plausible/blob/main/packages/clickhouse/ch-user-config.xml) to tune things up for Railway, and a [`railway.json` file](https://github.com/railwayapp-templates/plausible/blob/main/packages/clickhouse/railway.json) to [define deployment configuration for the service](https://docs.railway.app/deploy/config-as-code).
- [PostgreSQL Database](https://www.postgresql.org/): the users, settings, and metadata database
  - PostgreSQL is used to store user data, settings, and metadata for Plausible Analytics.
  - PostgreSQL is ran as one of [Railway's one-click database services](https://docs.railway.app/develop/services#database-services) and is just a standard PostgreSQL database.

## Additional resources

If you'd like to customize your instance of Plausible Analytics, I would recommend reviewing the documentation for both ClickHouse DB, and Plausible Analytics. Here are some links to get you started:

- [Plausible welcome guide](https://plausible.io/docs/)
- [Plausible self-hosting docs](https://plausible.io/docs/self-hosting-configuration)
- [ClickHouse docker docs](https://hub.docker.com/r/clickhouse/clickhouse-server/)

## Feedback

If you experience any issues or have any feedback at all, [you can create a GitHub issue here](https://github.com/railwayapp-templates/plausible/issues)

### Known issues

None right now! 
