---
layout: post
title: "Rails Console: Useful tricks"
date: 2013-07-24 22:22
comments: true
categories:
published: true
---
The past couple of weeks I've been engaged in what could be best described as a love/hate relationship with the Rails console. I'm not alone. At times, it can be your best friend, other times it can leave you bewildered, frustrated, and wishing you had a bat. But it's not always console's fault, you have to know how to help console help you. There are a few tricks which can go a long way to helping you do that. Following are a few of the more useful and interesting ones.

Let's start with a few oldies but goodies. `reload!` will reload your Rails environment in the console enabling any changes to your app's models to be reflected. Much less annoying than exiting and then restarting the console every time you make a change. If what your seeing in the console output just doesn't make any sense, it may not be a bad idea to execute `reload!` just in case your console environment needs updating. No guarantees but every so often it does the trick.

When you have a need to experiment but are worried about placing your database in great peril, have no fear, `rails c --sandbox` is there to alleviate your fears. Starting the console with the `--sandbox` option places your console environment in "sandbox" mode. Any database changes which occur while you're in this mode will be rolled back when you exit. You can be as reckless as you want. Rails console has you covered.

In Rails console, the underscore, `_`, has never been more useful. In console, `_` represents the output of the last command run. How often do you run a command with the intent of assigning the output to a variable but forget the variable assignment. That is situation where `_` shines. You can assign the aforementioned variable with the command output by entering `foo = _`.

Now for one of my favorites. It's very easy to remember, the letter `y`. If you place a `y` ahead of your command (`y User.first`), the output will load to YAML. The resulting formatting makes the output immensely easier to read. This works with most model objects and data structures. `y` is worth it's virtual weight in gold when dealing with nested hashes.

`helper` can be used to access Rails helper methods in the console. For example, `helper.pluralize(3, 'dog')` results in `"3 dogs"`. `helper.number_to_currency(25.32)` results in `"$25.32"`. `helper.link_to 'Sign out', '/sign_out'` results in `"<a href=\"/sign_out\">Sign out</a>"`.

The `app` object can be used to access your controllers through the console. For example, `app.new_user_path` returns `"/users/new"`. `app.cookies` returns a Rails CookieJar object with which you can access session cookie data.

And last but not least, I can highly recommend Ryan Bates' Railscast ["Console Tricks"](http://railscasts.com/episodes/48-console-tricks-revised).
