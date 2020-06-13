---
layout: post
title:      "Reflections - My first Rails Application"
date:       2020-06-13 18:52:41 +0000
permalink:  reflections_-_my_first_rails_application
---



What a journey! Rails has been quite the framework that has put me on some challenging roads however I am grateful for all that I have learnt and applied.

As with every project/app, I begin with what purposeful application I would like to build. I wanted to create an application that allows users to sign up, add their inspirational/spiritual books to their profile and finally add their reflective thoughts on these books.

Which models and attributes do I need then? Simple: User, Books & Reflections. 

A user would have many books, many reflections and many "reflected" books through reflections.

```
  has_many :owned_books, foreign_key: :owner_user_id, class_name: "Book"
  has_many :reflections, foreign_key: :reflection_user_id
  has_many :reflection_books, through: :reflections
```

A books would belong to a user, have many reflections and many "reflection" users through reflections. I also included a `has_one_attached :image` in order to upload a book cover image for each book.

```
  has_one_attached :image
  has_many :reflections, foreign_key: :reflection_book_id
  has_many :reflection_users, through: :reflections
  belongs_to :owner_user, class_name: "User", optional: true
```

A reflection would belong to both a user and a book.

```
  belongs_to :reflection_user, class_name: "User"
  belongs_to :reflection_book, class_name: "Book"
```

After creating the database and association models, I moved onto the routes that are required and then I worked on my controllers. 
Working on the controller methods, I saw a lot of repetition and we all know the drill...DRY! So, I either created before action methods under `private` and helper methods in my `application_controller.rb` file.

For example, in my User controller:

```
  class UsersController < ApplicationController
  ...
  before_action :set_user, only: [:show, :edit, :settings, :destroy]

  ...
	
	private

  def set_user
    @user = User.find(params[:id])
  end

  def access_self
    if @user = current_user
      @user
    end
  end

  def user_params
    params.require(:user).permit(:username, :password, :email)
  end

end
```

I had to deal a lot with `form_for` which is a brillant helper to create forms requiring models. `Form_for` is pretty neat when dealing with validation errors as you can simply call the instance variable with `.errors` to get standard error messages. 
Apart from `form_for`, I also saw many `button_to` helpers across my application. DRY, DRY, you guessed it...DRY!

I had to find a way to clean up my app and so used partials to help me access embedded ruby code across my erb files and create helper methods, where necessary.

I must admit, that the scope method took a lot of thinking power as I seemed to over complicate what I was trying to achieve. My aim was to join the `reflections` table with my `users` > access every `user` that has at least one `reflection` > show the `user`'s in descending order from the time they were created > show the particular `user` with the `book` that they just reflected on. Well...yeah 🙃
So instead I did:

```
  scope :with_reflections, ->{ joins(:reflections).order(created_at: :DESC) }
```

Which does everything I wanted except for showing the particular `user` with the `book` that they just reflected on. I can live with that, not too bad. 😁

I love the idea of nested routes and objects. What a brilliant way of associating objects smoothly. First step: create the nested routes:

  (In my case)
	
```
  resources :books do
    resources :reflections, only: [:new, :edit, :show]
  end
```

Next, using `build` within my controller to associate the `reflection` with the `book`:

```
  @reflection = @book.reflections.build
```

Then, seeing the lovely URL e.g., 

```
  http://localhost:3000/books/42/reflections/39
```


I saw many similarities with Sinatra and at times, I was extremely lost when hands on with the project but what a great way to learn hey - being stuck and tackling through it! I'm looking forward to the next project and creating other rails web applications! 💻

