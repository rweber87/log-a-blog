---
layout: post
title:  "Operation: Ghost Town"
date:   2017-05-03 15:30:04 -0400
categories: Turning Nothing Into Something
---

May the fourth be with you!

![current_users](https://rweber87.github.io/log-a-blog/assets/post3/vaderMeme.png)

My friend [Dave](https://github.com/drumnation) and I used our newly aqcuired coding jedi skills and worked on an application together replicating a reddit like website with one big exception. It was full of fake news! You're probably saying to yourself, "Why does the world need another fake news website?!" We wanted to bring about fake news in a clearly obvious way by illustrating how unbelievable these articles actually were. It also highlights how easily we can abuse our jedi powers for evil by propensiating bad or fake content.

In the process of creating our app we had one issue that was important to make our site more believable. We needed users so our website had a little more street credibility. But how were we going to generate users out of thin air? Thanks for our wonderful gem library we were able to do just that! The three gems that made this possible were [factory-helper](https://rubygems.org/gems/factory-helper/versions/1.7.4), [faker](https://rubygems.org/gems/faker) and [ui_faces](https://rubygems.org/gems/ui_faces)! They're really easy to install as most gems are, except these don't work very well together. To utilize and seed your database you'll have to use them separately or you'll run into kinks like [Dave](https://github.com/drumnation) and I.

First, you'll want to include each gem in the gem file of your application and run `bundle install`. Once that's done you'll need to create the seed file with the relevant information for each of your users. We had some fun and gave our users Chuck Norris quotes when they loaded, beer names, a "Harry Potter" location, and a few other random facts about them that aren't relevant at all (see how ridiculously fun this is becoming?!)

The app as it stands currently has one user, myself.

![current_users](https://rweber87.github.io/log-a-blog/assets/post3/current_users.png)

To begin generating our users we'll want to create a seeds file to actually persist the users into our database that will later be rendered when visited.

```ruby
require 'ui_faces'
require 'factory-helper'

100.times do
  def generate_gender
    random_gender = Random.new.rand(0..1)
  end

  def male_or_female(binary)
    binary == 0 ? "male" : 'female'
  end

  @gender = male_or_female(generate_gender)

  def male_name_or_female_name
    if @gender == "male"
      FactoryHelper::Name.male_first_name
    elsif @gender == "female"
      FactoryHelper::Name.female_first_name
    end
  end

	User.create(
		name: male_name_or_female_name,
		username: FactoryHelper::Internet.user_name(male_name_or_female_name),
		email: FactoryHelper::Internet.email(male_name_or_female_name),
		password: FactoryHelper::Internet.password,
		gender: @gender,
		image: UiFaces.sex(@gender),
		city: FactoryHelper::Address.city,
		zip: FactoryHelper::Address.zip
	)
end

```

At the top of our seeds file we're including two gems [ui_faces](https://rubygems.org/gems/ui_faces) and [factory-helper](https://rubygems.org/gems/factory-helper/versions/1.7.4). The [ui_faces](https://rubygems.org/gems/ui_faces) gem persists random images of users. We wanted an assortment of male and female users so we added a helper method that signaled to our `User create` method which type of name to generate. This allowed us to specify the image and email to be gender specific as well. As you can see we're calling this generate method 100 times to seed 100 new users into our database. The fun part is watching all of these user persist and knowing our town is slowly coming to life.

![generateUserGif](https://rweber87.github.io/log-a-blog/assets/post3/generateUserGif.gif)

The next step (and this was just for giggles) was using the [faker](https://rubygems.org/gems/faker) gem to give each user some unique facts that make absolutely no sense. That seed file looked something like this...

```ruby
require 'faker'

User.all.each do |user|
  user.update(
  	book_genre: Faker::Book.genre,
		chuck_norris_fact: Faker::ChuckNorris.fact,
		beer_name: Faker::Beer.name,
		food_ingredient: Faker::Food.ingredient,
		gameofthrones_house: Faker::GameOfThrones.house,
		harry_potter_location: Faker::HarryPotter.location,
		job_key_skill: Faker::Job.key_skill,
		space_planet: Faker::Space.planet
  )
end
```

Each user will now have random information in their "About Me" section of our app stating what type of novel they'd be, the type of beer they prefer, a wise fact from Chuck Norris etc. This only further illustrates the ridiculous nature of our application.

Let's watch this bit persist to each user that exists!

![extraUserData](https://rweber87.github.io/log-a-blog/assets/post3/extraUserData.gif)

The moral of our jedi story is to not take for granted the power of the internet at our fingertips. It's easy to turn our ways towards the dark side and convince people that nothing is something for recognition's sake.

![happyVaderMeme](https://rweber87.github.io/log-a-blog/assets/post3/happyVaderMeme.png)

Questions or comments? Feel free to shoot me an email (click the link below).

[Github](https://github.com/rweber87)
[Email](rob.weber87@gmail.com)

<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->