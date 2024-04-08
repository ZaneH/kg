---
title: Dokku (Self-Hosted Heroku)
---

Every wanted to host your own version of Heroku? Dokku is a self-hosted Platform as a Service (PaaS) that allows you to deploy, manage, and scale your applications. It's a great alternative to Heroku and provides a lot of flexibility in terms of deployment options. I got it running on a VPS and have been using it to deploy various applications. A couple months ago, I would've been paying \$5 per app per month, but now I can host as many apps as I want for \$5/mo. Here's how to get started with Dokku:

> [!info]
> I recommend creating a separate user for Dokku to run as. This will help with security and permissions. This user will likely need to have sudo privileges.

## Setup to Deployment

1. Install Dokku on your server by following the instructions on the [official website](https://dokku.com/docs/getting-started/installation/).
2. Determine if you want to use the Procfile or Dockerfile for your application. I prefer the Procfile because it's simpler and easier to manage. Depending on which you choose will determine a lot of the deployment process and configuration.
3. Create a new app by running `dokku apps:create <app-name>`.
4. Add a remote to your local git repository by running `git remote add dokku dokku@<server-ip>:<app-name>`.

Once done, you can deploy your application by running `git push dokku main`. The following sections will cover some of the main features I needed to get started with Dokku.

## Procfile

A Procfile is typically very simple, I typically default to the following:

```bash title="Procfile"
web: [command-to-start-your-app]
```

`web` is a special name that tells Dokku to automatically scale it to 1 instance rather than having to manually run it.

## Environment Variables

Environment variables can be set by running `dokku config:set <app-name> <key>=<value>`. You can also set multiple at once by running `dokku config:set <app-name> <key1>=<value1> <key2>=<value2>`. To view the environment variables, run `dokku config <app-name>`.

I *think* when working with the Dockerfile deployment method, environment variables work slightly differently, I believe they must be set as build args. Check [the Dokku docs here](https://dokku.com/docs/deployment/builders/dockerfiles/#build-time-configuration-variables).

Part of the reason I'm sticking to Procfiles for now.

## Linking Databases

Linking a database is as simple as installing a plugin and running a command.

```bash
sudo dokku plugin:install https://github.com/dokku/dokku-mongo.git mongo
dokku mongo:create [db-name]
dokku mongo:link [db-name] [app-name]
```

This will automatically set the `MONGO_URL` environment variable for your app.

## Connect MongoDB Compass thru SSH

I really like to have an easy GUI for my databases if I can. MongoDB Compass is a great tool for this, but connecting to a remote MongoDB instance can be a bit tricky.

I expected this to work the same way as it would had I ran the MongoDB service in Docker, however, turns out the MongoDB service is only exposed internally by default. To fix this, I ran:

```bash
dokku mongo:unexpose [app-name] # Unexpose the default ports
dokku mongo:expose [app-name] 127.0.0.1:27017 27018 27019 28017
```

Then the following settings work:

```bash
mongodb://<user>:<password>@localhost:27017/<database>
```

### Advanced Connection Options
- Proxy/SSH: SSH with Password (or Identity File)
    - Hostname: Remote VPS IP
    - Port: 22
    - Username: dokku (or the user running Dokku)

## Make Sure Only One Process is Running

While working with some of my apps, I noticed that some will break if more than one instance is running. This happens when deploying a new version of the app while the old one is still running (aka Zero Downtime Deployment). To disable this, I ran:

```bash
dokku checks:disable [app-name] web
```

This way, it stops the old instance before starting the new one.