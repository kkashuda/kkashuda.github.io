---
layout: post
title:  "Rails Portfolio Project "
date:   2017-05-22 16:14:09 -0400
---


## What is Rails? 

Rails is a powerful web framework with a lot of underlying magic. Rails, in a nutshell, is a web framework, a ruby gem, and an MVC framework. It provides the tools developers need to develop applications, consisting of a set of Ruby libraries with a set application architecture to help developers with separation of concerns. 

## Getting Started with Rails 

Since Rails is a ruby gem you need to install it on your system to run and develop rails applications. To install rails on your system, run the command `gem install rails` 

To create a new rails application run the following command in your terminal: 

`rails new application-name`

Now if you view the directories and files created you will see the directory application of every rails application. 

Running the command `rails s` will start up the server. If you navigate to http://localhost:3000/ you will see the rails  'Yay! You're on Rails!' page that ships with Rails letting you know you are ready to start building your application. 

## Building a Rails Application 

Once I set up the rails framework for my portfolio project, it was time to create the models and respective tables. Rails has some nice generators to help simplify setup. My project is a Pinterest clone so I started by building a pins table. Using the following command I generated the Pin model and pins table: 

`rails g model pin title:string description:text`

### Authentication 

Then I set up authentication using Devise. Adding the gem 'devise' to my Gemfile and running `rails generate devise:install
` generated the files for devise authentication. I then created the User model using devise by running: `rails generate devise user` At this point, I was able to add the navigation links to have user functionality in my application. 


### has_many, a belongs_to, and has_many :through

Relationships between models take a bit of thinking and physically drawing out in my case. In rails, these relationships between models are referred to as *associations*. Once you figure out these associations, the logic of your app becomes much simpler. 

Here are the associations I came up with for my application: 

```
class Pin < ApplicationRecord
  belongs_to :user 
  belongs_to :category
```

```
class Category < ApplicationRecord
  has_many :pins 
  has_many :users, through: :pins 
```

```
class User < ApplicationRecord
  has_many :users
  has_many :pins 
  has_many :categories, through: :pins 
```

Assuming @user is a user object, associations allow for things like `@user.pins`and `@user.pins.first.category.name` assuming "name" is an attribute of Category. Having these associations makes it very convenient to do a multitude of common operations you'd want to perform when building an application. 

The has many through association is special in that it creates a join between two models. In this case, Category joins the Pin and User model. This sets up what is known as a many to many connection between the models. That is, the declaring model is able to have zero or more instances of another model through a third model. 

### Validations

Validations are used to ensure that only valid data is saved to the database. There are a number of macros you can use in your rails application to accomplish this. For example in my user's model I ensure the email is unique through the following validation: 

```
  validates :email, uniqueness: true, on: :create
```

The on: :create allows me to edit a user's account and save the account with the existing email, while still ensuring that when a new user creates an account, the email is unique. 

This next set of validations handles my Pin model. You can set length validations, presence validations as well as format validations using regular expressions. 

```
  validates :title, length: { minimum: 5 }
  validates :title, presence: true 
  validates :description, presence: true 
  validates :link, :format => URI::regexp(%w(http https)), :allow_blank => true
```

To verify that a particular attribute is valid you can use `errors[:attribute]`. This returns an array of error messages that you can then display in your views. Assuming we have an instance of the Pin model saved in @pin here is how you would display error messages in a view: 

```
<% if @pin.errors.any? %>
  <div id="error_explanation">
    <h2><%= pluralize(@pin.errors.count, "error") %> prohibited this article from being saved:</h2>
 
    <ul>
    <% @pin.errors.full_messages.each do |msg| %>
      <li><%= msg %></li>
    <% end %>
    </ul>
  </div>
<% end %>
```


### Setting Attributes in ActiveRecord 

Building a form in rails consists of using a FormBuilder object allowing you to generate fields for a particular model's attributes.  This allows for nested attributes as well. That is, accessing a parent models attribute when generating a field for a model that is inheriting from a parent model. This is where strong parameters come in. Strong parameters essentially sanitize data coming in when mass assigning. Here is an example of handling strong parameters with nested attributes: 

```
    def pin_params
       params.require(:pin).permit(:title, :description, :image, :category, :link, category_attributes: [:name])
    end
```

category_attributes: is an attribute setter defined in my Pin model as: 

```
  def category_attributes=(category)
    self.category = Category.find_or_create_by(name: category["name"])
    self.category.update(category)
  end
```


### OAuth

Omniauth is a gem that allows for multiple forms of authentication for an application. It allows for username and password, Facebook, Google and more using OAuth protocol. OAuth is an industry standard authentication allowing for third party services to be used for authentication purposes. Omniauth takes OAuth, and makes it relatively easy to set up third-party login options for your site. In my case, I used Facebook as a secondary login option. Here is a link to a site giving a detailed tutorial on how to set it up: [omniauth facebook setup](http://richonrails.com/articles/facebook-authentication-in-ruby-on-rails) 

## Do Not Repeat Yourself (DRY) 

DRY or Do Not Repeat Yourself is a well-known principle in software development to help cut down on duplicate code. For example, when designing views in a rails application, it is common to need the same elements in multiple views. Using partial templates can help eliminate this duplicate code. By default filenames of partial templates are saved with the name beginning with an underscore. In your view you can then access the partial like so: `render partial: partial_name path` When referencing the partial you omit the beginning underscore, and the path refers to the location of the partial. 


## In Conclusion

As you can see, there are a lot of different components when building out a rails application. Luckily, many of the standards have been set, which helps cut down development time. I look forward to continuing working with rails and learning more about it. There's a lot to potentially learn! 











            
            




