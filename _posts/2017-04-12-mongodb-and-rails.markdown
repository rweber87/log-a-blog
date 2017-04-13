---
layout: post
title:  "MongoDB and Rails"
date:   2017-04-12 15:30:04 -0400
categories: Integrating MongoDB with Rails
---

First step to setting up Mongo on your rails app is install Mongo. Follow this [documentation](https://www.mongodb.com/download-center#production).

Once the installation is complete setting up Mongo to be used in your rails application has never been easier! When setting up an application quickly we'll run our command `rails new app_name` command with one exception - we need to include `--skip-active-record` to ensure it doesn't conflict with setting up our Mongo database.

![Installation](https://rweber87.github.io/log-a-blog/assets/post2/installation.png)

Next we'll want to include this line of code in our in our /config/application.rb file `Mongoid.load!('config/mongoid.yml')` along with the gem in our gem file ensuring the Mongo version is the most recent one followed by running `bundle install`.

![Gem](https://rweber87.github.io/log-a-blog/assets/post2/gemversion.png)

This gem offers us a convenient method to generate a config file for our DB `rails g mongoid:config`. We can leave the config with it's default options but it comes with a lot of written comments to further explore some things you can pass in.

For demonstration purposes I've gone ahead and generated a quick scaffold of a product model for our website with a name as a string type and price as a `big_decimal`. Mongoid overrides the model generators with it's own. Let's take a look:

![ModelBefore](https://rweber87.github.io/log-a-blog/assets/post2/modelbefore.png)

Here we see a similar setup to our migration tasks with one exception - __this is our model file__! Another great win with utilizing Mongo is there is no need to stage a migration to update your database because the schema doesn't exist (it does but very loosely). Our database is entirely flexible based on how we want to customize our web application.

![ModelAfter](https://rweber87.github.io/log-a-blog/assets/post2/modelafter.png)

If we want to change our schema to the product model we merely add a field attribute to the model class called `:released_on` with a data type of `Date`. This new update has now given us an additional attribute for our products that allow us to track when the product was released! One thing to remember is ensuring your schema permits this new field column for when you're persisting data. 

One of the added benefits to using MongoDB for your DBMS is the flexibility to embed related data types into one document. Let's say we wanted to create a review for a product we're selling on our website. In a relational database system we'd have to generate a separate table to house the information related to reviews via a migration, a separate model, as well as controller. With Mongo we simply generate the model for reviews then utilize the Active Record-esque macros to call those attributes. For our example we want to include a review for a product. To do so we generate our reviews model and include `embedded_in :product` on our product model and `embeds_many :reviews` in our product model. This again offers us those ActiveRecord macros to be able to call reviews on a product similar to before`product.reviews`. 

![Embedsmany](https://rweber87.github.io/log-a-blog/assets/post2/embedsmany.png)

![Review](https://rweber87.github.io/log-a-blog/assets/post2/reviews.png)

Other great features offered by Mongo are it's simple and easy way to query data. In the example below we're running a query on our products to return everything that has a price less than or equal to 40 (Mongo syntax => lte) `Product.where(:price.lte => 40)`. Another way to write that is to run the query on the class directly `Product.lte(price: 40).first`. The abbreviated syntax again offers the user to focus on Mongo syntax as opposed to remembering the Active Record methods that come out of the box, and IMO reads slightly better. Refer to this link for more ways to query using [MongoDB](https://docs.mongodb.com/ruby-driver/master/tutorials/6.1.0/mongoid-queries/)

![Query](https://rweber87.github.io/log-a-blog/assets/post2/querying.png)

[Github](https://github.com/rweber87)
[Email](rob.weber87@gmail.com)




<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->