---
layout: post
title: Backup PostgreSQL from AppFog
excerpt: "How to backup your PostgreSQL database from AppFog"
comments: true
---

Backing up a PostgreSQL database from AppFog is as easy as typing two commands:

af login
{% highlight bash %}
Attempting login to [https://api.appfog.com]
Email: [YOUR_EMAIL]
Password: [YOUR_PASSWORD]
Successfully logged into [https://api.appfog.com]
{% endhighlight %}

af export-service \[POSTGRESQL_DATABASE\]

{% highlight bash %}
Exporting data from '[POSTGRESQL_DATABASE]': OK
http://dl.eu01.aws.af.cm/serialized/postgresql/[DATABASE]/snapshots/[FILE_NUMBER]?token=[TOKEN]
{% endhighlight %}

## Restore using pg_restore

If you want to restore that backup in your localhost, then just execute the following command:

{% highlight bash %}
pg_restore -c -d [POSTGRESQL_DATABASE] -U [USERNAME] -W [DUMP_FILE]
{% endhighlight %}

\[YOUR_DUMP_FILE\] is inside the file that you just downloaded when you exported the database.

These are the meanings of the flags used:

-c
--clean
Clean (drop) database objects before recreating them.

-d dbname
--dbname=dbname
Connect to database dbname and restore directly into the database.

-U username
--username=username
User name to connect as.

-W
--password
Force pg_restore to prompt for a password before connecting to a database.

You can read more documentation http://www.postgresql.org/docs/8.4/static/app-pgrestore.html

Restore on AppFog with pg_dump & pg_restore

PGPASSWORD=\[LOCALHOST_PASSWORD\] pg_dump -Fc --no-acl --no-owner -h localhost -U \[LOCALHOST_USERNAME\] \[DEVELOPMENT_DB\] > \[DEVELOPMENT_DB\].dump

Upload the .dump to your AppFog

RAILS_ENV=proxied-appfog pg_restore --verbose --clean --no-acl --no-owner -h localhost -p \[PORT\] -d \[POSTGRESQL_DATABASE\] -U \[USERNAME\] \[DUMP_FILE\]