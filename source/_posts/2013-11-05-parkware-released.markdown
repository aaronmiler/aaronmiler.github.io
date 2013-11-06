---
layout: post
title: "ParkWare Released"
date: 2013-11-05 18:55
comments: true
categories: RubyMotion ParkWare iOS App
---

ParkWare finally got approved by Apple and is now avalible on the [App Store](https://itunes.apple.com/us/app/parkware/id729283928). Hooray!

I can't quite decide which direction to take this blog post. I've started to write about the app, as well as about developing the app. I decided that I'm going to cover both sides here. 

<!-- more -->

<div style="max-width:250px;width:25%;float:right;margin:10px;"><img src="/images/blog/parkware_app_store.jpg" width="100%" /></div>

### About the App

ParkWare is an app to track where you parked your car using your phones GPS. While there are apps on the app store that already accomplish this. There is a specific problem I wanted to solve. 

My girlfriend and I share a car, and one of the questions I get almost every day is "Where did we park the car?". The solution to this problem, was an app we could both use on our iPhones, and we could park/locate the same car.

ParkWare identifies a car using a unique 8 digit HEX code. Users can change this code within the settings page, and if they use the same code as another user. It allows them to share a car, parking and locating the same car using the API.

### Developing the App

ParkWare was made with RubyMotion. My whole lifetime as a web developer has been spent making things for the web. So this was the first time that I was able to make something almost tangable. This was a great feeling for me, and the fact that I could use Ruby was an added bonus.

Something I really liked about RubyMotion, is the fact that it compiles to machine code. Meaning there is no interperater.

While the community seems very small, and most the google queries for problems come up with Objective-C answers. I still enjoyed using it very much. After a using RubyMotion for a while, I was able to look at Objective-C/iPhone documentation, and adapt it to RubyMotion code. 

All in all I'm just much happier while writing Ruby code. While learning the idocincrosis of iOS within RubyMotion was congusing at first. I have to say I feel as if the code I've written is quite readable, and I had fun doing it. I've still got quite a bit of refactoring to do. But it's something I'm enjoying writing.