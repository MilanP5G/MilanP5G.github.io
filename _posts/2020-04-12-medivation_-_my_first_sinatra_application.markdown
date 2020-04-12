---
layout: post
title:      "Medivation - My first Sinatra Application"
date:       2020-04-12 11:25:52 -0400
permalink:  medivation_-_my_first_sinatra_application
---


![Medivation Logo](https://imgur.com/301Leh0)


This was a great journey, one where I felt I had more of an idea of where I wanted to take my project and learnt a lot along the way.

I wanted to create an application that has a similar function to already existing social platforms such as Facebook, Twitter etc. but centres solely around meditative and motivational messages to share and read ("inspire and be inspired"). 

My first thought was the models I would need and how they relate to each other. The two models I created were `Users` and `Posts`. Their relationship, you ask? A `User` would have many posts and `Posts` would belong to a user.

`class User < ActiveRecord::Base`
  `has_secure_password`
  `has_many :posts`

  `validates :username, presence: true`
  `validates :email, presence: true`
  `validates :password, presence: true`

`end`

`class Post < ActiveRecord::Base`
 `belongs_to :user`

 `validates :title, presence: true`
 `validates :content, presence: true`

`end`

Using ActiveRecord would connect my application to a database and allow my Models to have certain attributes that are written out in the `Users` and `Posts` tables, For example:

`class CreateUsers < ActiveRecord::Migration[6.0]`
  `def change`
   `create_table :users do | t |`
     `t.string :username`
      `t.string :email`
     `t.string :password_digest`
    `end`
 `end`
`end`

Before I created any of the .erb files and started working on the .rb files that connect with each other, I first created the `Helpers` class along with its methods. The `Helpers` methods would ensure that certain functions are only allowed if a `User` is logged in or if it is the current user (who is logged in) carrying out an action.

The `Helpers` methods:
`class Helpers`

   `def self.current_user(session)`
     `@user = User.find_by_id(session[:user_id])`
   `end`

   `def self.logged_in?(session)`
     `!!session[:user_id]`
   `end`

`end`

The first method is checking if the `session[:user_id]` belongs to the user id and if so, that user can carry out certain actions which I will come to later*. The second method is checking if the `session[:user_id]` is operating.

Then I moved onto creating my `GET`, `POST`, `PATCH` and `DELETE` routes along with the respective view files. I used the `Helpers` methods in a few of my route methods. This section allowed me to become more familiar with Ruby and its functions. Allowing me to create nested if statements, nested iterations and even both of them combined which I have not really explored as much before. 

Now coming onto the "certain actions" that are accessible by the `current_user` or if the user is `logged_in?`. These actions are known as **CRUD** - **C**reate, **R**ead, **U**pdate and **D**elete. I had to work with RESTful routes and give access to all these operations to a user that is `logged_in?` and if they are the `current_user`.  For example: 

`patch '/users/:id' do`
   ` user = User.find_by(id: params["id"])`
   ` if user == Helpers.current_user(session)`
     ` user.update(params[:user])`
     ` redirect "/settings"`
    `else`
      `redirect "/home"`
    `end`
  `end`
	
This PATCH route allows the user to **U**pdate their own profile (in this case, their username, email and/or password). I create a local variable called user that equals to the `find_by` method on the User class which searches for a user by their id. Next I use an `if` statement that checks to see if the user's id links with the current user's id. If it does, then the user can update their profile - this is done by accessing the parameters of the user which are username, email and password. If this is all successful, then the user, once updating their profile, would be sent back to the settings page. However, if this is not successful due to there not being a current user and session, then they are directed to the home page (this home page is what a user first sees without being logged in).

This project was a very long one but I appreciate every step as I have learnt many things that I can apply for more projects to come.

