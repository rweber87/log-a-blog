---
layout: post
title:  "Testing in Ruby with RSpec"
date:   2017-06-30 15:30:04 -0400
categories: RSpec Ruby Testing
---

The topic of writing your own tests has been frequently coming up in the last few lectures/coding meetup events I've attended. It had me thinking about my deficiency in writing tests for my own projects. One of the best ways I've found to learn is start a mini project and write my own tests.

For this example we're going to start with creating a single class and writing specifications (specs for short) for an instance to pass. Let's build an animal class that has three parameters that need to be passed in upon initialization for a valid instance. Before that we'll need to create our project and add our `spec gem` to write the necessary tests. 

I've created a directory called `zoo_project` and ran the command `gem install rspec` to add our testing framework.

![makingdirectory](https://rweber87.github.io/log-a-blog/assets/post5/makingdirectory.png)

Next we'll need a `spec` directory to hold all the testing files we'll be writing. We will also need the actual class file to creat instances of that particular class for testing purposes. In case you haven't guessed it yet, we'll be creating classes of animals to add to our 'zoo' project.

![helperfiles](https://rweber87.github.io/log-a-blog/assets/post5/helperfiles.png)

In our `spec_helper.rb` file we can include the `animal.rb` file's relative path so it knows how to implement the tests we'll be writing. At the top of the file include the line `require_relatve '../animal'`.

Now let's get writing some actual tests for our `Animal` class. We can namespace the tests we want to write for our `Animal` class by writing our initial block as follows...

```ruby
require 'spec_helper'

describe Animal do

  before :each do
    @animal = Animal.new "type", "age", "category"
  end
  
end
```

Here we've described what we'll be testing - in this case it's our `Animal` class we're testing that takes a block of code `do` and `end`. The way this is structured tells the user the tests that follow this line of code are meant for that specific class. We've also included a `before` block.  A `before` block of code is run before any of the tests are executed as they will be dependent on an instance of an `Animal`.

Let's now write a test that describes that our `new` method should be an instance of the `Animal` class.

```ruby
require 'spec_helper'

describe Animal do

  before :each do
    @animal = Animal.new "type", "age", "category"
  end


  describe "#new" do 
    it "returns a new animal object" do
      expect(@animal).to be_an_instance_of Animal
    end

    it "throws an ArgumentError when given fewer than 3 parameters" do 
      expect {Animal.new "type", "age"}.to raise_exception ArgumentError
    end
  end

end
```



[Github](https://github.com/rweber87)
[Email](rob.weber87@gmail.com)

<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->