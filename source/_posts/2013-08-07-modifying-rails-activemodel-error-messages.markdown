---
layout: post
title: "Modifying Rails ActiveModel Error Messages"
date: 2013-08-08 23:53
comments: true
categories:
published: true
---

Recently I was applying some validations to models on a Rails application I'm currently working on when I found myself in a bit of a double pickle. I had a need to get rid of an ActiveModel error message that was being generated and add one that wasn't. How do you do either of those? Let me tell you how you can do both.

In Rails, when you try saving an object to a database or execute the `.valid?` method on it, if any model validations fail, error messages are written to an ActiveModel errors hash. This hash can be accessed by executing `.errors.messages` on the object. So let's say you have a `@user` object you execute `@user.save` or `@user.valid?` on, after doing so, you can execute `@user.errors.messages` to check for any error messages. The resulting hash will look something like the following:
``` ruby
{:name=>["can't be blank"],
:email=>["can't be blank"],
:email_confirmation=>["can't be blank"],
:password=>["can't be blank"],
:password_confirmation=>["can't be blank"],
:password_digest=>["can't be blank"]}
```
This hash comes in handy to display the error messages to the user. Rails makes it even easier with the `.full_messages` method. For the errors hash above, `@user.errors.full_messages` results in

``` ruby
["Name can't be blank",
"Email can't be blank",
"Email confirmation can't be blank",
"Password can't be blank",
"Password confirmation can't be blank",
"Password digest can't be blank"]
```
Iterating through this array and printing the error messages is a snap. But ...

What if you don't want to print one or more of these error messages? For example, "Password digest can't be blank". That message will very well leave many a user scratching their head. Let's get rid of it from the hash. `@user.errors.delete(:password_digest)` will do the trick. You can use `.errors.delete(:key)` to delete any of the messages in the errors hash.

``` ruby
["Name can't be blank",
"Email can't be blank",
"Email confirmation can't be blank",
"Password can't be blank",
"Password confirmation can't be blank"]
```

The error messages that are automatically generated result from failed validations on model attributes of the object in question. But what about validations you perform on any associations or any non-standard validations? If any of those validations fail and you want a message included in the ActiveModel errors hash, you have to add it in yourself.

In my situation, I performed a validation on a 'roles' association with my User model. Since the validation was not on an attribute of my `User` model, if the validation failed an error message would not be automatically generated and added to the errors hash. So after a little research I wound up using `@user.errors[:base] << "error message"`. This added my message to the hash and made it available in the `@user.errors.full_messages` array. That easy.

And, should you want to, you can also add additional messages associated with specific model attributes in the same way. For example, if I performed some validation checking that the name entered is all lower-case, on failure I could execute `@user.errors[:name] << "must be all lower-case"`. The resulting messages array winds up looking as follows:

``` ruby
["Name can't be blank",
"Name must be all lower case",
"Email can't be blank",
"Email confirmation can't be blank",
"Password can't be blank",
"Password confirmation can't be blank",
"Password digest can't be blank"]
```

