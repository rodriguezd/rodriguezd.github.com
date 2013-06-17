---
layout: post
title: "Can one ever know too many command line tricks?"
date: 2013-06-16 18:37
comments: true
categories:
published: true
---

I don't think so either.

Looking through some presentation decks on [speakerdeck.com](https://speakerdeck.com/), I came across two presentations addressing this which I can never can get enough of. The two decks are "[Unix Command Line Productivity Tips](https://speakerdeck.com/keithrbennett/unix-command-line-productivity-tips)" by Keith Bennet and "[Time-saving tricks on the command line](https://speakerdeck.com/janosgyerik/time-saving-tricks-on-the-command-line)" by Janos Gyerik.

Following are some of the command line gems I gathered from their presentations. If you are unfamiliar with any of them, I strongly encourage you to try them out. I suspect you will like what you find.

* **cd -**

(The dash is part of the command) Ever find yourself jumping back and forth between two directories? This puppy toggles the current and previous directory.

* **pushd** and **popd**

Pushd is short for 'push directory' and popd for 'pop directory'. If you execute **'pushd .'** and then move to a different directory, you can then execute **'popd'** and it will take you back to the directory you pushed previously. How cool is that?!?

* **!$**

Not pretty but this captures the last parameter in the previously executed commad. For example, if you **'touch file.txt'** and then **'subl !$'**, Sublime Text opens **file.txt**.

###For your editing on the commad line pleasure:

* **ctrl - w**

Deletes the last word you have entered on the commad line

* **ctrl - k**

Deletes from the cursor position to the end of the line

* **ctrl - y**

Pastes whatever you deleted in the previous commad

* **cntrl-a**

Jump to the start of the line

* **cntrl - e**

Jump to the end of the line.

* **option - left/right**

Skip left/right one word at a time


Enjoy.