---
title: "PostgreSQL"
date: 2019-07-21T13:09:06+09:00
draft: true
tags:
  - dev
---

I have a habit of doing `brew update` every week. It's a been a while since I've used PostgreSQL, last I remember it was version 9, now it's 11 and I can't connect to it because of some migration issues.

`psql: could not connect to server: No such file or directory`

Since I installed it using homebrew, the easy way to fix it is to use the included upgrade script.

`brew postgresql-upgrade-database`

## Quick memory refresher

- `psql`: shortcut for connecting to PostgreSQL with defaults
- `psql -h localhost -p 5432 -U $USER_NAME $DB_NAME`: the entire command
- `createdb $DB_NAME`: creates a DB from **outside** psql
- `CREATE DATABASE $DB_NAME`: creates a DB from inside psql
- `\l`: list all databases
- `\c $DB_NAME`: connect to database
- `\du`: show a list of all users
- `\d`: show list of tables
- `\q`: quit

## Use a GUI

`brew cask install pg4admin`

Then go make some tea. This takes a while.
