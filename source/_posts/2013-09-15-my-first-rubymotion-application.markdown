---
layout: post
title: "My First Rubymotion Application"
date: 2013-09-15 16:22
comments: true
categories: ios rubymotion ruby
---

After struggling to figure out Rubymotion for a while. I found a [great set of tutorials](http://rubymotion-tutorial.com/) by Clay Allsopp. 

With these examples, and the rest of the internet to help me. I was able to frakenstien enough things together to create an application.

<!-- more -->

Meet Parquare

![Parquare](/images/parquare.png)

Parquare is an application that you can use for remembering where you parked your car. With a [supporting API](https://github.com/aaronmiler/car_app_api) the thing that makes this iPhone app stand out is the ability to share your car code with another person.

Now hopefully you don't park your car on a highway. But if you do, Parquare will remember where you parked it.

While the application works. I'm pretty sure that my code is a mess. Regardless, there are a couple of things I figured out and found helpful. Here are a couple of snippets

Button with an Image Background
``` ruby
@back_btn = UIButton.buttonWithType UIButtonTypeCustom
@back_btn.frame = [[0,0], [122, 40]]
@back_btn.setBackgroundImage(UIImage.imageNamed("btn_home_locate"), forState: UIControlStateNormal)
```

I often used this for centering objects within my view window
``` ruby
@THING.center = CGPointMake(self.view.frame.size.width / 2, Y)
```
Making a label wrap was tricky. But this seemed to do the trick. 
``` ruby
@update = UILabel.alloc.init
@update.lineBreakMode = UILineBreakModeWordWrap
@update.numberOfLines = 2 # Or if set to 0, allows for any number of lines
@update.frame = [[20,165],[300,100]]
```

Adding an image to the view
``` ruby
@image = UIImageView.alloc.initWithFrame([[100, 150],[258, 57]])
@image.image = UIImage.imageNamed("image")
```

Another thing that made a lot more sense after I looked it up was Frames. When first playing with the numbers I thought they were (X1,Y1),(X2,Y2). When it turns out that a fame is actually [[Xpos,Ypos],[Width,Height]].

Every time I do something in Rubymotion I feel like I'm learning more. As time goes I hope to make more applications and make a better use of this excellent tool. 

I haven't released the application to the App Store yet, I still think I have some design changes to make. But as soon as I do it will be interesting to see if any bug reports come in. I am also going to start refactoring my code shortly after I release it.