---
layout: post
title: "Sharing Partials Across Models In Rails"
date: 2013-08-21 08:56
comments: true
categories:
published: true
---

So yesterday I was working on a Rails side project and I found myself in a situation where I had a partial that I wanted to use in several different views spanning several different models. My first impulse was just to place a copy of the partial in each of the models' views folders but that felt very wrong. Not very "dry" at all. There had to be a better way. It took me about ten seconds of research to come upon a perfect solution. The kind of solution that as soon as you read about it you knock yourself on the forehead and go "Duuuuuuuuhhh!".

The best thing to do is to create a "shared" subdirectory under `app/views`. Technically you can name the subdirectory whatever you want but "shared" seems so right. (DHH himself has also endorsed this approach.) And then you place all your shared partials in this new directory. Then in your code instead of `render 'partial'` you just have to `render 'shared/partial'`. That simple.