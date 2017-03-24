---
layout: post
title:  "DBMS - What is it and which is right for me?"
date:   2017-03-23 15:30:04 -0400
categories: jekyll update
---

DBMS stands for database management system (acronyms ftw!). Simply put it's a way for users to interact with data. A common misconception when learning about DBMS is referring to them as the database itself. It's actually an intermediary between the user, data, and other applications to capture and analyze data sets. During your journey as a developer you will likely reach a moment where you'll need to ask yourself "self: which DBMS should I use?" My goal is to shine some light on the pro's and cons of some popular ones that are out there for you to better reach that conclusion on your own. 

Three examples of commonly used DBMS' in today's development world are SQLite, MySQL, and MongoDB.

![SQLite](https://rweber87.github.io/log-a-blog/assets/SQLite.png)

SQLite is a neat little [RDBMS](https://en.wikipedia.org/wiki/Relational_database_management_system) released in 2000. A unique aspect of SQLite is it is embedded in the application running SQL as opposed to a client server database engine. This means it is tightly integrated in the application and makes calls to files that contain the data locally as opposed to a server. That alone makes SQLite very compact and portable for basic querying analysis, but at a cost.

Because of how portable this DBMS is it's ability to handle [multi-user](https://en.wikipedia.org/wiki/Multi-user) applications are limited. If you're looking for scalable DBMS's that can handle multiple users or high writing volume this one is likely not a good fit. 

![MySQL](https://rweber87.github.io/log-a-blog/assets/MySQL.png)
 
MySQL is ranked #2 in terms [popularity](http://db-engines.com/en/ranking_trend) just behind Oracle. As you might have assumed, MySQL is built to handle larger volumes of data and users.  It comes with many of the standard SQL features one would expect when using a [RDBMS](https://en.wikipedia.org/wiki/Relational_database_management_system)  and also comes with a more advanced built-in security interface. 

Limitations when considering MySQL is it's inflexible nature at using storage engines other than the default InnoDB. You give up some of the standard SQL functionality when using other databases ["including foreign key references and check constraints."](https://en.wikipedia.org/wiki/MySQL)

The general consensus seems that MySQL's ease of use through open-sourced tools has helped it reach the level of popularity it has gained today.

A few companies currently utilizing MySQL include sites such as `Google, Facebook, Twitter, Flickr, and YouTube`.

![MongoDB](https://rweber87.github.io/log-a-blog/assets/MongoDB.png)

The key difference that sets the other reviewed DBMS from Mongo is it is a *NoSQL document-oriented database program* (now that's a mouthful!). What does that mean exactly? Well let's break it down:

* NoSQL - Does not imply what you might think. The "No" actually stands for Not Only. In other words SQL isn't the only language accepted to write queries. All that being said, Mongo does *not* support SQL when running queries. 

* Document-oriented database implies that, unlike it's sibling relational databases (table based), all of our data can be stored in one single instance in the database. This allows the task of mapping to be quite flexible. [Here's a great article comparing document oriented databses vs. relational oriented databases.](http://docs.couchbase.com/developer/dev-guide-3.0/compare-docs-vs-relational.html)

Additionally, the syntax of writing Mongo queries are quite different from SQL and seem very method like.

A standard SQL query such as...
{% highlight ruby %}
SELECT * FROM inventory WHERE status = "D"
{% endhighlight %}

Would be re-written as...
{% highlight ruby %}
db.inventory.find( { status: "D" } )
{% endhighlight %}

Mongo also supports a vast majority of popular langues out there...

![MongoDBLanguages](https://rweber87.github.io/log-a-blog/assets/MongoLanguages.jpg)

Some downsides to this language (which is entirely subjective): the lack of structure makes it difficult to standardize for users. There also lacks a good security configuration which resulted in DB's being stolen and held for ransom.

All-in-all it's really up to you and the application you're trying to build. In my opinion it seems best to start small and work your way up as needed, but don't wait too long to upgrade or integrating a new system to fit your needs could prove to be quite difficult.

Here's a fun mapping of Facebook's class design. Enjoy!

![FacebookSchema](https://rweber87.github.io/log-a-blog/assets/facebookschema.jpg)

[source](http://web.archive.org/web/20121031052327/http://blogs.x2line.com/al/archive/2007/06/02/3124.aspx)



<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->