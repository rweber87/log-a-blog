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

Next we'll need a `spec` directory to hold all the testing files we'll be writing. We will also need the actual class file to creat instances of that particular class for testing purposes. 

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

The `describe '#new' do ` block is very readable, very Ruby, and does exactly as it sounds. We're writing tests within this block of code to ensure the new method returns an `Animal` object and throws an error if an incorrect number of parameters are passed on the initialize method. Before we can test our tests, we'll need to define our `Animal` class and write the intialize method. In our `animal.rb` file add this line of code.

```ruby
class Animal

  def initialize(type, age, category)
    @type = type
    @age = age
    @category = category
  end

end
```
Now we can see if our two tests we've written actually work. Run this line of code in the home directory `rspec spec --format doc`.

![firsttest](https://rweber87.github.io/log-a-blog/assets/post5/firstest.png)

Awesome! Green is always a good sign when testing. For our last bit in this tutorial let's go ahead and write tests for the actual attributes we want an `Animal` to possess. 

Add these tests just below the `#new` block of tests so we can ensure the attributes of an `Animal` align with `before :each` `Animal` instance.

```ruby
  describe "@type" do
    it "returns the correct Type" do
      expect(@animal.type).to eq "type"
    end
  end

  describe "@age" do
    it "returns the correct Age" do
      expect(@animal.age).to eq "age"
    end
  end

  describe "@category" do
    it "returns the correct Type" do
      expect(@animal.category).to eq "category"
    end
  end
```

Here we're describing what the return value should be when we've set up our `Animal` initialize method correctly. Each attribute should return their respective value as defined in our `before :each` block of code. The last thing we need to do is define those methods on our `Animal` class. The easy way to do so is through our `attr_accessor` methods. Add this line of code above the initialize method to our `animal.rb` file `attr_accessor :type, :age, :category`. Let's run our test one final time and ensure all is right with our mini project.

![lasttest](https://rweber87.github.io/log-a-blog/assets/post5/lasttest.png)


[Github](https://github.com/rweber87)
[Email](rob.weber87@gmail.com)

<!-- Mapping for links :D [jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
 -->