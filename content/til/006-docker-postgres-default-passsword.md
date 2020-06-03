---
title: "006 Docker Postgres default password"
date: 2020-06-03T00:00:00+09:00
tags:
  - til
  - docker
  - postgres
  - continuum
---

I'm not sure when this change was added. When starting up a container without a password set, the container will silently fail. This message will appear in the logs.

```
Error: Database is uninitialized and superuser password is not specified.
       You must specify POSTGRES_PASSWORD for the superuser. Use
       "-e POSTGRES_PASSWORD=password" to set it in "docker run".

       You may also use POSTGRES_HOST_AUTH_METHOD=trust to allow all connections
       without a password. This is *not* recommended. See PostgreSQL
       documentation about "trust":
       https://www.postgresql.org/docs/current/auth-trust.html

```

Problem can be solved by adding `POSTGRES_HOST_AUTH_METHOD=trust` to the commands.

reference: https://github.com/thelegendofcode/continuum/compare/29232e7d2641...774450c9a368
