---
layout: post
title: PostgreSQL Case Sensitivity for a Rails Active Record Query
---

PostgreSQL has case sensitivity and converts column names to lowercase when trying to do an Active Record Query. An error like the one below will occur:

{% highlight bash %}
  PG::Error: ERROR:  column "some_column" does not exist
LINE 1: SELECT "some_table".* FROM "some_table"  WHERE (SOME_UPPERCASE_COLUMN = 'some_value')
{% endhighlight %}

In order to solve this problem just escape quotes, likes this:

{% highlight ruby %}
  Class.all(conditions: ["\"SOME_UPPERCASE_COLUMN\" = ?", 'some_value'])
{% endhighlight %}

Problem fixed!