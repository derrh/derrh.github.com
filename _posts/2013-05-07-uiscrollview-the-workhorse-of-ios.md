---
layout: post
title: "UIScrollView: The Workhorse of iOS"
description: ""
summary: "Whenever I set out to do anything that involves panning, pinching or zooming, I always ask myself: \"Can I just use a UIScrollView for that?\""
category: iOS
tags: [uiscrollview, uitableviewcell, swipe]
---
{% include JB/setup %}
Whenever I set out to do anything that involves panning, pinching or zooming, I always ask myself: "Can I just use a UIScrollView for that?"

There are plenty of places where UIScrollView is the obvious choice. But I find myself using it even when it doesn't seem so obvious as a solution.

In a personal app that I am working on, I wanted to have `UITableViewCell` sliding similar to [Mailbox](http://mailboxapp.com). I started out by adding a container view to a custom `UITableViewCell` and then attaching a `UIPanGestureRecognizer` to that. This worked pretty well, but the code gets pretty messy especially if you want to have the inertial scrolling and paging behavior that we have come to know and love from `UIScrollView`. Then it hit me: why not try adding a `UIScrollView` instead of sort of rolling my own.

I was pretty happy with [the result](https://github.com/derrh/SwipeAwayCell), and will be using this in my own app.

