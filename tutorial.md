# Introduction

Hey guys, I am Terian and we are going to build together a super awesome and  hot web app in this series. The app will be based on Ruby on Rails API flavored by AngularJS. As a bonus we will follow Google's trendy [Material Design](http://www.google.com/design/spec/material-design/introduction.html) guidelines and use appropriate frameworks.

I will walk you through three basic steps, here they are!

1. Build a simple API with Ruby on Rails,
2. Create AngularJS services/controllers based on this API,
3. Apply Material Design framework to the app.

Eventually we will end up with a web app looking something like this:

![Screenshot](http://i.imgur.com/UVTJc60.png)

PUT A GIF HERE!

Looking nice, huh? So are you ready to roll?


## Put em on Rails

In this section I'll talk about setting up a simple Ruby on Rails back-end assuming you are familiar with the framework. Even though I will not fall into details that much, you are free to add comments, questions right after this article.

*Any comments, suggestions or questions are much appreciated!*

Okay, let's start. First of all we need to define our app, it's functionality and requirements. Before going deep into terminology let's try to summarize what our app is for? What problem does it solve?

Taskey is a task tracking web app that lets **users** post **tasks** setting some ammout of money they are willing to pay for that **task**. **Users** can view all available **tasks**, add **comments** or **bids**. Then **task** poster can decide whom to assign a **task**. Once a **task** is assigned to a specific **user** its status is changed to 'assigned', after changed to 'closed' upon completion.

Pretty straightforward eh? Look closely, we have almost defined our models while describing our app! so lets put the words in Rails way
- Users has_many Tasks
- Tasks has_many Comments
- Tasks has_many Bids

As simple as that!
Let's start from the models.

### Models

#### Users
First thing first, we'll start from the **users**. Add Devise Token Auth gem ADD LINK HERE to your Gemfile, we'll use it for authentication. Now we can generate **users** model:

```
rails generate devise_token_auth:install User auth
```

Our **users** model should look like:

```
class User < ActiveRecord::Base
  devise	:database_authenticatable,
  			:registerable,
  			:recoverable,
  			:rememberable,
  			:trackable,
  			:validatable
  include DeviseTokenAuth::Concerns::User

  has_many :tasks, dependent: :destroy
end
```

#### Tasks, Comments and Bids
**task**, **comment** and **bid** models are pretty simple:

```
class Task < ActiveRecord::Base
	belongs_to :user
end
```


### Routes
We will add a api scope in our routes to serve JSON data for AngularJS.

```
  scope '/api' do
    mount_devise_token_auth_for 'User', at: '/auth'
      resources :tasks, defaults: { format: :json }
  end
```













Once we have our models we can define our controllers. We will use basic CRUD controllers. A template looks like this:

```
	def index
		respond_with Task.all
	end

	def create
		task = Task.new(task_params)
		task.save
		
		respond_with task
	end

	def update
		task = Task.find(params[:id])
		task.update_attributes(task_params)
	end

	def show
		task = Task.find(params[:id])
		respond_with task
	end

	def destroy
		task = Task.find(params[:id]).destroy
		respond_with Task.all
	end
	
```




