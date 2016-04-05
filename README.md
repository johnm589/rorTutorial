# How to build a Ruby on rails C.R.U.D app

The purpose of this lesson is to teach you how to make a very basic CRUD app. This lesson will cover a very simplistic Instagram knock-off built with Ruby on Rails

## What is CRUD?

Crud stands for: Create, Read, Update, Destroy. 

Many apps follow this basic model: Twitter, Craigslist, Facebook and Instagram are all CRUD apps. 

By the end of this lesson we should know how to build a website that allows a user to: Create posts that include a title, a body and a picture. They will be able to view (READ)that post, and edit(UPDATE) it and delete (DESTROY) it. 

## Let's start

Whats the first thing we do to start a RoR app?

###### rails new appName

CD into the appName and let's have a look at what we got.

Now lets open the file in your favorite text editor and run the rails server.

######rails s

##Git in it

Now lets get into git before we get too far. 

#####git init
#####git add .
##### git commit - m "init" 

Good, now we can screw up and be able to revert if need be. Be sure to always commit early and commit often when your'e making a big project like this.

## Posts

Since our app will focus entirely on posts. Lets generate the controller for posts.

###### rails g controller posts

Now lets go into the controller we just created and add the following ruby code:

```
def index 
end
```

This is just a placeholder for a function we will add later.

## Resource Routing

Resource routing is a super easy way to cover most of the common bases when establishing routes. 

######resources:posts

This command covers a variety of routes for Posts which we created earlier. You can read more about resource routing in the documentation 
[here.](http://guides.rubyonrails.org/routing.html#resource-routing-the-rails-default)

Let's also declare index.html.erb to be our root:

######root 'posts#index'  


Now lets create a view index.html.erb under views so we can make sure this worked. 


```<h1>myApp!</h1>
```

##Database

Now let's get our database set up

For now let's just get our title and body of our posts squared away.

######rails g model Post title:string body:string

This creates a database that will accept 2 parameters one is called "title" and the other "body". We've also specified that they will both be strings.

Now that we've created the data base, let's DB seed + migrate.

######rake db:seed
######rake db:migrate

## Pics or it Didn't Happen

Now were going to add the image functionality. Let's download a gem to help us with this: 

###### gem 'paperclip'

Now add this code to the posts controller

```
  has_attached_file :image
```

You can also add validators if need be but its not nessecary for this app

This specifies that an image is attached to posts 

We now need to do a migration for images. There are multiple ways to do this but the easiest i think is 

######rails g paperclip post image

(I'm actually not sure why this step needs to happen but it is in the docs)

##Forms

First lets install a gem called 'simple form'

This gem just makes forms a little simpler. this isnt necessary, but it makes creating forms in rails much easier.

Create a new file (new.html.erb)

and use this code

```
<%= simple_form_for @post do |f| %>
  <%= f.input :image %>
  <%= f.input :title %>
  <%= f.input :body %>
  <%= f.button :submit %>
<% end %>
```
Here we are creating a form for the user to input data to the database. Notice that it takes inputs for image, title, body (all models we created) and finally a submit button.			


