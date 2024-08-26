### Step-1: Make Directory `chatwoot_coolify`
```
mkdir chatwoot_coolify && cd chatwoot_coolify
```
### Step-2: Download `ChatWoot` `.env.example` file as `.env`
```
wget -O .env https://raw.githubusercontent.com/chatwoot/chatwoot/develop/.env.example
```
### Step-3: Download `ChatWoot` `docker-compose.production.yaml` file as `docker-compose.yaml`
```
wget -O docker-compose.yaml https://raw.githubusercontent.com/chatwoot/chatwoot/develop/docker-compose.production.yaml
```
### Step-4: Download `rails.sh`
```
wget -O rails.sh https://raw.githubusercontent.com/chatwoot/chatwoot/develop/docker/entrypoints/rails.sh
```
### Step-5: Open `.env` file in a editor and Modify it as following
```shell
# Learn about the various environment variables at
# https://www.chatwoot.com/docs/self-hosted/configuration/environment-variables/#rails-production-variables

# Used to verify the integrity of signed cookies. so ensure a secure value is set
# SECRET_KEY_BASE should be alphanumeric. Avoid special characters or symbols. 
# Use `rake secret` to generate this variable
SECRET_KEY_BASE=replace_with_lengthy_secure_hex

# Replace with the URL you are planning to use for your app
FRONTEND_URL=http://0.0.0.0:3000
# To use a dedicated URL for help center pages
# HELPCENTER_URL=http://0.0.0.0:3000

# If the variable is set, all non-authenticated pages would fallback to the default locale.
# Whenever a new account is created, the default language will be DEFAULT_LOCALE instead of en
# DEFAULT_LOCALE=en

# If you plan to use CDN for your assets, set Asset CDN Host
ASSET_CDN_HOST=

# Force all access to the app over SSL, default is set to false
FORCE_SSL=false

# This lets you control new sign ups on your chatwoot installation
# true : default option, allows sign ups
# false : disables all the end points related to sign ups
# api_only: disables the UI for signup, but you can create sign ups via the account apis
ENABLE_ACCOUNT_SIGNUP=false

# Redis config
# specify the configs via single URL or individual variables
# ref: https://www.iana.org/assignments/uri-schemes/prov/redis
# You can also use the following format for the URL: redis://:password@host:port/db_number
REDIS_URL=redis://redis:6379
# If you are using docker-compose, set this variable's value to be any string,
# which will be the password for the redis service running inside the docker-compose
# to make it secure
REDIS_PASSWORD=R@@@kin_007
# Redis Sentinel can be used by passing list of sentinel host and ports e,g. sentinel_host1:port1,sentinel_host2:port2
REDIS_SENTINELS=
# Redis sentinel master name is required when using sentinel, default value is "mymaster".
# You can find list of master using "SENTINEL masters" command
REDIS_SENTINEL_MASTER_NAME=

# By default Chatwoot will pass REDIS_PASSWORD as the password value for sentinels
# Use the following environment variable to customize passwords for sentinels.
# Use empty string if sentinels are configured with out passwords
# REDIS_SENTINEL_PASSWORD=

# Redis premium breakage in heroku fix
# enable the following configuration
# ref: https://github.com/chatwoot/chatwoot/issues/2420
# REDIS_OPENSSL_VERIFY_MODE=none

# Postgres Database config variables
# You can leave POSTGRES_DATABASE blank. The default name of
# the database in the production environment is chatwoot_production
POSTGRES_DATABASE=
POSTGRES_HOST=postgres
POSTGRES_USERNAME=postgres
POSTGRES_PASSWORD=R@@kin_007
RAILS_ENV=development
# Changes the Postgres query timeout limit. The default is 14 seconds. Modify only when required.
# POSTGRES_STATEMENT_TIMEOUT=14s
RAILS_MAX_THREADS=5

# The email from which all outgoing emails are sent
# could user either  `email@yourdomain.com` or `BrandName <email@yourdomain.com>`
MAILER_SENDER_EMAIL=Chatwoot <accounts@chatwoot.com>

#SMTP domain key is set up for HELO checking
SMTP_DOMAIN=chatwoot.com
# Set the value to "mailhog" if using docker-compose for development environments,
# Set the value as "localhost" or your SMTP address in other environments
# If SMTP_ADDRESS is empty, Chatwoot would try to use sendmail(postfix)
SMTP_ADDRESS=
SMTP_PORT=1025
SMTP_USERNAME=
SMTP_PASSWORD=
# plain,login,cram_md5
SMTP_AUTHENTICATION=
SMTP_ENABLE_STARTTLS_AUTO=true
# Can be: 'none', 'peer', 'client_once', 'fail_if_no_peer_cert', see http://api.rubyonrails.org/classes/ActionMailer/Base.html
SMTP_OPENSSL_VERIFY_MODE=peer
# Comment out the following environment variables if required by your SMTP server
# SMTP_TLS=
# SMTP_SSL=
# SMTP_OPEN_TIMEOUT
# SMTP_READ_TIMEOUT

# Mail Incoming
# This is the domain set for the reply emails when conversation continuity is enabled
MAILER_INBOUND_EMAIL_DOMAIN=
# Set this to the appropriate ingress channel with regards to incoming emails
# Possible values are :
# relay for Exim, Postfix, Qmail
# mailgun for Mailgun
# mandrill for Mandrill
# postmark for Postmark
# sendgrid for Sendgrid
RAILS_INBOUND_EMAIL_SERVICE=
# Use one of the following based on the email ingress service
# Ref: https://edgeguides.rubyonrails.org/action_mailbox_basics.html
# Set this to a password of your choice and use it in the Inbound webhook
RAILS_INBOUND_EMAIL_PASSWORD=

MAILGUN_INGRESS_SIGNING_KEY=
MANDRILL_INGRESS_API_KEY=

# Creating Your Inbound Webhook Instructions for Postmark and Sendgrid:
# Inbound webhook URL format:
#    https://actionmailbox:[YOUR_RAILS_INBOUND_EMAIL_PASSWORD]@[YOUR_CHATWOOT_DOMAIN.COM]/rails/action_mailbox/[RAILS_INBOUND_EMAIL_SERVICE]/inbound_emails
# Note: Replace the values inside the brackets; do not include the brackets themselves.
# Example: https://actionmailbox:mYRandomPassword3@chatwoot.example.com/rails/action_mailbox/postmark/inbound_emails
# For Postmark
# Ensure the 'Include raw email content in JSON payload' checkbox is selected in the inbound webhook section.

# Storage
ACTIVE_STORAGE_SERVICE=local

# Amazon S3
# documentation: https://www.chatwoot.com/docs/configuring-s3-bucket-as-cloud-storage
S3_BUCKET_NAME=
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=

# Log settings
# Disable if you want to write logs to a file
RAILS_LOG_TO_STDOUT=true
LOG_LEVEL=info
LOG_SIZE=500
# Configure this environment variable if you want to use lograge instead of rails logger
#LOGRAGE_ENABLED=true

### This environment variables are only required if you are setting up social media channels

# Facebook
# documentation: https://www.chatwoot.com/docs/facebook-setup
FB_VERIFY_TOKEN=
FB_APP_SECRET=
FB_APP_ID=

# https://developers.facebook.com/docs/messenger-platform/instagram/get-started#app-dashboard
IG_VERIFY_TOKEN=

# Twitter
# documentation: https://www.chatwoot.com/docs/twitter-app-setup
TWITTER_APP_ID=
TWITTER_CONSUMER_KEY=
TWITTER_CONSUMER_SECRET=
TWITTER_ENVIRONMENT=

#slack integration
SLACK_CLIENT_ID=
SLACK_CLIENT_SECRET=

# Google OAuth
GOOGLE_OAUTH_CLIENT_ID=
GOOGLE_OAUTH_CLIENT_SECRET=
GOOGLE_OAUTH_CALLBACK_URL=

### Change this env variable only if you are using a custom build mobile app
## Mobile app env variables
IOS_APP_ID=L7YLMN4634.com.chatwoot.app
ANDROID_BUNDLE_ID=com.chatwoot.app

# https://developers.google.com/android/guides/client-auth (use keytool to print the fingerprint in the first section)
ANDROID_SHA256_CERT_FINGERPRINT=AC:73:8E:DE:EB:56:EA:CC:10:87:02:A7:65:37:7B:38:D4:5D:D4:53:F8:3B:FB:D3:C6:28:64:1D:AA:08:1E:D8

### Smart App Banner
# https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html
# You can find your app-id in https://itunesconnect.apple.com
#IOS_APP_IDENTIFIER=1495796682

## Push Notification
## generate a new key value here : https://d3v.one/vapid-key-generator/
# VAPID_PUBLIC_KEY=
# VAPID_PRIVATE_KEY=
#
# for mobile apps
# FCM_SERVER_KEY=

### APM and Error Monitoring configurations
## Elastic APM
## https://www.elastic.co/guide/en/apm/agent/ruby/current/getting-started-rails.html
# ELASTIC_APM_SERVER_URL=
# ELASTIC_APM_SECRET_TOKEN=

## Sentry
# SENTRY_DSN=


## Scout
## https://scoutapm.com/docs/ruby/configuration
# SCOUT_KEY=YOURKEY
# SCOUT_NAME=YOURAPPNAME (Production)
# SCOUT_MONITOR=true

## NewRelic
# https://docs.newrelic.com/docs/agents/ruby-agent/configuration/ruby-agent-configuration/
# NEW_RELIC_LICENSE_KEY=
# Set this to true to allow newrelic apm to send logs.
# This is turned off by default.
# NEW_RELIC_APPLICATION_LOGGING_ENABLED=

## Datadog
## https://github.com/DataDog/dd-trace-rb/blob/master/docs/GettingStarted.md#environment-variables
# DD_TRACE_AGENT_URL=

# MaxMindDB API key to download GeoLite2 City database
# IP_LOOKUP_API_KEY=

## Rack Attack configuration
## To prevent and throttle abusive requests
# ENABLE_RACK_ATTACK=true
# RACK_ATTACK_LIMIT=300
# ENABLE_RACK_ATTACK_WIDGET_API=true

## Running chatwoot as an API only server
## setting this value to true will disable the frontend dashboard endpoints
# CW_API_ONLY_SERVER=false

## Development Only Config
# if you want to use letter_opener for local emails
# LETTER_OPENER=true
# meant to be used in github codespaces
# WEBPACKER_DEV_SERVER_PUBLIC=

# If you want to use official mobile app,
# the notifications would be relayed via a Chatwoot server
ENABLE_PUSH_RELAY_SERVER=true

# Stripe API key
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=

# Set to true if you want to upload files to cloud storage using the signed url
# Make sure to follow https://edgeguides.rubyonrails.org/active_storage_overview.html#cross-origin-resource-sharing-cors-configuration on the cloud storage after setting this to true.
DIRECT_UPLOADS_ENABLED=

#MS OAUTH creds
AZURE_APP_ID=
AZURE_APP_SECRET=

## Advanced configurations
## Change these values to fine tune performance
# control the concurrency setting of sidekiq
# SIDEKIQ_CONCURRENCY=10


# AI powered features
## OpenAI key
# OPENAI_API_KEY=

# Housekeeping/Performance related configurations
# Set to true if you want to remove stale contact inboxes
# contact_inboxes with no conversation older than 90 days will be removed
# REMOVE_STALE_CONTACT_INBOX_JOB_STATUS=false
```
### Step-6: Open `docker-compose.yaml` file in a editor and Modify it as following:-

```shell
services:
  base: &base
    image: chatwoot/chatwoot:latest
    env_file: .env ## Change this file for customized env variables
    volumes:
      - ./data/storage:/app/storage

  rails:
    <<: *base
    depends_on:
      - postgres
      - redis
    ports:
      - '127.0.0.1:3010:3000'
    environment:
      - NODE_ENV=production
      - RAILS_ENV=production
      - INSTALLATION_ENV=docker
    entrypoint: ./rails.sh
    # command: ['bundle', 'exec', 'rails', 's', '-p', '3000', '-b', '0.0.0.0']
    command: >
      /bin/sh -c "bundle exec rails db:chatwoot_prepare && bundle exec rails s -p 3000 -b 0.0.0.0"
    restart: always

  sidekiq:
    <<: *base
    depends_on:
      - postgres
      - redis
    environment:
      - NODE_ENV=production
      - RAILS_ENV=production
      - INSTALLATION_ENV=docker
    command: ['bundle', 'exec', 'sidekiq', '-C', 'config/sidekiq.yml']
    restart: always

  postgres:
    image: postgres:12
    restart: always
    ports:
      - '127.0.0.1:5432:5432'
    volumes:
      - ./data/postgres:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=${POSTGRES_DATABASE}
      - POSTGRES_USER=${POSTGRES_USERNAME}
      # Please provide your own password.
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}

  redis:
    image: redis:alpine
    restart: always
    command: ["sh", "-c", "redis-server --requirepass \"$REDIS_PASSWORD\""]
    env_file: .env
    volumes:
      - ./data/redis:/data
    ports:
      - '127.0.0.1:6379:6379'
```
### Step-7: Create a repository named`chatwoot_coolify` on Github and push the local changes into it
- `git init`
- `git remote add origin https://github.com/SajidK25/chatwoot_coolify.git`
- `git add -A`
- `git commit -m 'local deployment okay'`
- `git push origin master`

## Step-8: Chatwoot Deployment Process on Coolify

### Step-8a: Add Docker registry

1. Go to `settings`.
2. Click `Docker registries` tab.
3. Click `Add Docker Registry`.
4. Name: Give registry a name.
5. URL: `https://hub.docker.com/`.
6. Username: Your Dockerhub username.
7. Password: Your Dockerhub password
8. Click on the `Save` button

![001.CoolifyAddDockerRegistry.png](./images/001.CoolifyAddDockerRegistry.png)

![002.CoolifyDockerRegistries.png](./images/002.CoolifyDockerRegistries.png)


### Step-8b: Create New Resource
1. Go to Dashboard and click `Create New Resource >> Application`.

![003.CoolifyDashBoardCreateNewResource.png](./images/003.CoolifyDashBoardCreateNewResource.png)

### Step-8c: Select an Application source
1. Public repository from the git: `https://github.com/SajidK25/chatwoot_coolify/blob/master`.
2. Click on the `Load Repository` Button

![004.CoolifyLoadRepo.png](./images/004.CoolifyLoadRepo.png)

### Step-8d: Select a Build Pack
1. Select a Build Pack `Docker Compose`.

![005.CoolifySelectABuildPack.png](./images/005.CoolifySelectABuildPack.png)

### Step-8e: Configuration General Tab
1. Docker Repository: `Select Your previously created Docker Repository`.
2. Name: `Chatwoot-app`

![006.ConfigGeneral.png](./images/006.ConfigGeneral.png)

### Step-8f: Configuration Stack `Rails`
1. URL (FQDN): `https://chatwoot.example.com`.
2. Port: `9001`.
3. Keep the other services unchanged.

![007.StackRails.png](images/007.StackRails.png)

### Step-8g: Configuration Stack `Rails`
1. Copy all environment variables from given `.env` file.
2. Paste on `Paste .env file` text area.
3. Click on button `Add Secrets in batch`.

![009.ClickOnTheDeployButton.png](images/009.ClickOnTheDeployButton.png)

### Step-8h: Deployment
1. Click on the top right corner's `Deploy` button.

![009.ClickOnTheDeployButton.png](images/009.ClickOnTheDeployButton.png)

2. After completing successful deployment process

![010.DeploymentSuccess.png](images/010.DeploymentSuccess.png)

3. Browse the URL: `https://chatwoot.example.com`. You can see the Login page

![004.ChatwootLogin.png](<images/004.ChatwootLogin.png>)

4. After login you might see the DashBoard

![003.ChatwootDashboard.png](images/003.ChatwootDashboard.png)

