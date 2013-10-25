---
layout: post
title: Including External Files on vBulletin Templates
categories:
- Blog
tags: []
status: publish
type: post
published: true
meta:
  _syntaxhighlighter_encoded: '1'
  _edit_last: '1'
  dsq_thread_id: '511164874'
---
If you want to include an external php file on your vBulletin templates you'll need more than just following this <a href="https://www.vbulletin.com/docs/html/templates_externalfiles">https://www.vbulletin.com/docs/html/templates_externalfiles</a>

Instead of just creating a plugin like:
{% highlight php %}
ob_start();
include('path/to/this/file/myfile.php');
$includedphp = ob_get_contents();
ob_end_clean();
{% endhighlight %}

You  will need to add a last line, as following:

{% highlight php %}
ob_start();
include('path/to/this/file/myfile.php');
$includedphp = ob_get_contents();
ob_end_clean();
vB_Template::preRegister('TEMPLATE',array('includedphp' =&gt; $includedphp));
{% endhighlight %}

You will have to change the "TEMPLATE" and "path/to/this/file/myfile.php" as fits your needs.