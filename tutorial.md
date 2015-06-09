# Introduction

Hey guys, I am Terian and we are going to build together a super awesome and  hot web app in this series. The app will be based on Ruby on Rails API flavored by AngularJS. As a bonus we will follow trendy material design guidelines and use appropriate frameworks.

I will walk you through three basic steps, here are they!

1. Build a simple API with Ruby on Rails,
2. Create AngularJS services/controllers based on this API,
3. Apply material design framework to the app.

At the end we will end up with a web app looking something like this:

![Screenshot](http://i.imgur.com/UVTJc60.png)

Looking nice, huh? So are you ready to roll?


## Put em on Rails

In this section I'll talk about setting up a simple Ruby on Rails back-end assuming that you are familiar with the framework. Even though, I will not fall into details that much, you are free to add comments, questions right after this article.

*Any comments, suggestions or questions are much appreciated!*

Okay, let's start. First of all we need to define our app, it's functionality and requirements. Before going deep into terminology let's try to summarize what our app is for? What problem does it solve?

Taskey is a task tracking web app that lets **users** post **tasks** specifying some ammout of money they are willing to pay for that **task**. **users** can view all available **tasks**, add **comments** or **bids**. Then **task** poster can decide whom to assign a **task**. Once a **task** is assigned to a specific **user** its status is changed to 'assigned', after chnaged to 'closed' upon completion.

Pretty straightforward eh? Look closely, we have almost defined our models while describing our app! so lets put the words in Rails way
- Users has_many Tasks
- Tasks has_many Comments
- Tasks has_many Bids

As simple as that! Once we have our models we can define our controllers. We will use basic CRUD controllers for each of our model. A template looks like this:

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




