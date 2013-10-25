---
layout: post
title: PostgreSQL Case Sensitivity for a Rails Active Record Query
categories:
- Blog
tags: []
status: publish
type: post
published: true
meta:
  _syntaxhighlighter_encoded: '1'
  _edit_last: '1'
  dsq_thread_id: '748084906'
  _yoast_wpseo_linkdex: '0'
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