---
layout: post
title: "When application.html.erb just doesn't cut it"
date: 2013-07-10 01:19
comments: true
categories:
published: true
---

Recently I was working on a Rails application on which I had a need to apply layouts to views other than the default `application.html.erb` alyout. The following is what I discovered on how to do that. (*I make no claim that the following are the only and/or best ways to do this. Rails being Rails there are probably at least ten additionals ways.*)

###Controller Level Layout

If you wish to use a different layout for all the views associated with a particular controller, you have two options. The first option is to create a new layout with the same name as the controller you wish to apply it to. For example, let's say you have a controller named `UsersController` in your app, you could place a layout file named `users.html.erb` in the `app/views/layouts` folder. Rails will then apply the `users.html.erb` layout to all the Users views.

The second option is to include `layout "alternate_layout"` in the controller's class defnition. The alternate layout file must be present in the `app/views/layouts` folder. In this case the file's name does not have to be the same as the controller's.

``` ruby
class UsersController < ApplicationController

layout "alternate_layout"

### controller code ###

end
```

###Action/View Specific Layouts

But what if you don't want to apply an alternative layout to an entire controller? What if you only want to apply it to specific views? You have a few options here also.

One option is to specify which controller actions an alternative layout is to be apllied to. You can do so like this:
``` ruby
class UsersController < ApplicationController

layout "alternate_layout", only: [:index, :show]

### controller code ###

end
```
`application.html.erb` will be applied to the remainder of the action views.

A second option is to add a method in your controller which determines which layout to use at run time.
``` ruby
class UsersController < ApplicationController

  layout :resolve_layout

  ### controller code ###

  private
  def :resolve_layout
    case action_name
      when 'show'
        'show_layout'
      when 'index'
        'index_layout'
      else
        'application'
      end
  end
end
```

And if you choose you can specify an alternative layout at the controller action level.
``` ruby
def show

  render :layout => 'show_layout'

  ### action code ###

end
```
