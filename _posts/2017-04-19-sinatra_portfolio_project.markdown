---
layout: post
title:  "Sinatra Portfolio Project"
date:   2017-04-19 00:42:17 +0000
---


The Sinatra Portfolio Project has been a lot of fun to work on. Sinatra itself is cool to work with, but can be complex at times. The general outline of the project was to create a CRUD app of your choice. An app that tracks something that you find useful in your life. 

#### first things first: 

The first step was coming up with an idea. I always feel like I am missing out on local events that you can't find out about through a simple google search. Small events such as local art festivals, live music at a small brewery, etc. With this in mind, I wrote an app that creates an ongoing list of local events that are posted by users that signup. Users are able to view all posts, post their own, edit their own and delete their own posts. 

#### now for the coding: 

Once I set up an empty repository for the project and stubbed out the project structure I began with the models. As of this writing, the two models my app need are a User model and a Post model. The one-to-many relationship between the two is that the user has many posts and each post belongs to a user. 

```
class User                                      class Post
  has_many :posts                                 belongs_to :user
end                                              end 
```


#### time to set up the database:

Now that I understand the relationships between my two models I can go ahead and initialize the database. We can do that using rake, and active record! Rake a handy gem that mimics a Make. Active Record is a tool for working with relational databases. It offers an ORM framework that wraps around a relational database. To make use of this we will set up our models to inherit from ActiveRecord::Base. This will bind our classes to the database and allow us to perform CRUD actions on the data. The data lives in tables, and each model corresponds to one table. We can initialize tables using the command `rake db:create_migration NAME=table_name.` Here's an example of a table I made for users: 

```
class CreateUsers < ActiveRecord::Migration[5.0]
  def change
    create_table :users do |t|
      t.string :username
      t.string :password_digest
      t.string :email
    end
  end
end

```


#### testing, testing: 

At this point, I decided I should see if my relationships were set up correctly. Using the gem *tux* I was able to enter data in the database and play around with it. Once everything looked good I moved on to the views and controllers. I set up a layout.erb page first off. This page, in particular, has elements that you want on every page in the application. It made sense to set up a nav bar, as well as some CSS styling to make things prettier and more user-friendly. Apparently, Sinatra looks for stylesheets and such in a directory named *public* that lies in the root of your project. Thanks, internet! 

I then created two directories within the views directory-- one for users and one for posts. Each had corresponding views for controller actions defined in the controllers. 


#### controllers, controllin': 

Within my controller's directory, I decided on having a controller for each table, along with the application controller. Each of the controllers that pair with a table inherits from the application controller. Within the application, controller houses the configurations (e.g. enabling sessions, setting the views, etc.) as well as helper methods. Once I got into the flow of creating views and the corresponding controllers I found the best way to work swiftly was through the use of the gems *shotgun* and *pry*. Shotgun allowed me to keep the server running while I made changes, and pry allowed me to work with controllers to make sure I was working with the data I thought I was working with. 


#### the basics are there: 

Once I got all of the requirements done, meaning the basics were working, I started thinking of future work I want to incorporate into the app. For example, a helpful search for keywords, and maybe categories for types of events. All in all building with Sinatra and Active Record was a lot of fun, and I look forward to working with it more! 




