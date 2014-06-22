---
layout: post
title: "Using Devise Invitable"
date: 2013-08-28 10:16
comments: true
categories: [Devise,Gem,Ruby,Authentication]
---

I love using Devise for application authentication. When I was creating the [Realtime QA Tool](https://github.com/quangoinc/realtime_qa) I needed to make sure that the sign up form wasn't publicly accessible. So I started doing a little bit of searching I found [Devise Invitable](https://github.com/scambra/devise_invitable). Devise invitable allows you to invite users via e-mail to your application. 

<!-- more -->

Without this gem the only way I could think of to invite users was to create their login myself, with a temporary password. Having done that with some services in the past. I felt like that was a very primitive solution, so I set out to find a better solution. 

That is when I found Devise Invitable. The documentation for Devise invitable is great, so getting up and running.

Start out with two simple commands

```
rails generate devise_invitable:install
rails generate devise_invitable MODEL
```

Update your devise model
``` ruby
class User < ActiveRecord::Base
  devise :database_authenticatable, :confirmable, :invitable
end
```

and you're good to go.

After Devise Invitable is installed and ready to go, I usually end up making an invitation action in one of my controllers. Devise Invitable does allow you to make a dedicated controller for it. But I find I can usually accomplish everything with a simple action that looks something like that

``` ruby
def invite_user
  @user = User.invite!(:email => params[:user][:email], :name => params[:user][:name])
  render :json => @user
end
```
Just like that, you can now invite users to your application.