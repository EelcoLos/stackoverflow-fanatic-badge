# StackOverflow Fanatic Badge Achiever 🥇
An automated way to get the "fanatic" badge, by running a node bot in a docker
container that will log into your account everyday and send reports of your
progression.

## Requirements
- docker, preferably on a vps that can run it for 100 days straight
- a stackoverflow account
- a mailgun account

## Setup
There are three ways to configure it.

### With a config file
Create a `conf.json` file based on `conf.example.json` and mount it as a volume
into the container:

```bash
docker run -d -v path/to/conf.json:/conf.json \
    --name fanatic-bot \
    garsaud/stack-overflow-fanatic-badge
```

## Through the interactive mode
Build the config file answering questions:

```bash
touch conf.json
docker run --rm -it -v ${PWD}/conf.json:/conf.json \
    garsaud/stack-overflow-fanatic-badge configure
```

![](https://user-images.githubusercontent.com/3667366/54071538-1785ef00-426e-11e9-8d98-37b24778df0e.png)

Then launch the bot:

```bash
docker run -d -v ${PWD}/conf.json:/conf.json \
    --name fanatic-bot \
    garsaud/stack-overflow-fanatic-badge
```

## With inline arguments
If you don’t mind inline passwords, it is possible to configure and launch the bot in one command:

```bash
docker run -d -it --name fanatic-bot \
    garsaud/stack-overflow-fanatic-badge configure-and-launch \
    --login "your-stackoverflow-email@example.com" \
    --password "your slackoverflow password" \
    --mailgun_api_key "key-xxxxx" \
    --mailgun_domain "xxxxx.mailgun.org" \
    --from "postmaster@xxxxx.mailgun.org" \
    --to "your-email@example.com" \
    --subject "[CRON] StackOverflow fanatic badge report"
```
