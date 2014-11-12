---
layout: post
title: An internal error occurred during: "IvyDE resolve".
---

If you're trying to run Vaadin by following [this](https://github.com/vaadin/vaadin#setting-up-eclipse-to-develop-vaadin-7) and using Eclipse 4.4.1 it is likely that you will get the following error message:

<!-- ![Vaadin IvyDE Error]({{ site.url }}/assets/vaadin-error-1.png "Vaadin IvyDE Error") -->

> An internal error occurred during: "IvyDE resolve".
> org.eclipse.osgi.internal.framework.EquinoxConfiguration$1 cannot be cast to java.lang.String


The problem is totally on IvyDE's side and has already been [documented](https://issues.apache.org/jira/browse/IVY-1487) and a fix has been [merged](https://github.com/apache/ant-ivy/commit/81fec3193ad12a0f78eb021c4a1548484595860b). Nonetheless, it is still not available in the official update site `http://www.apache.org/dist/ant/ivyde/updatesite`. Thus, if you want to fix this issue you can use the [trunk version](http://ant.apache.org/ivy/ivyde/download.cgi#jenkins) of IvyDE.

Go to _Help > Install New Software..._

![Install New Software]({{ site.url }}/assets/vaadin-error-2.png "Install New Software")

Then enter `https://builds.apache.org/job/IvyDE-updatesite/lastSuccessfulBuild/artifact/trunk/build/` in the _Work with:_ field.

![Install New Software]({{ site.url }}/assets/vaadin-error-3.png "Install New Software")

Finally, select `Apache Ivy Library` and click Finnish.

Now you can import the Vaadin project, or if that was already done you can resolve the issues by using the options on vaadin project and choosing _Ivy > Resolve_

![Ivy Resolve]({{ site.url }}/assets/vaadin-error-4.png "Ivy Resolve")

Have fun with Vaadin!
