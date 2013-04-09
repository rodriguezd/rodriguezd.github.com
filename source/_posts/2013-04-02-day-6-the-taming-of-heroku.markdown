---
layout: post
title: "Day 6: The Taming of Heroku"
date: 2013-04-02 15:19
comments: true
categories:
published: true
---
Last night I told myself that I was not going to spend more than a half-hour today trying to finish deploying my Help A Cause app on Heroku. That's what I told myself. I meant it to. I really did.

I started off reading some from the *Learning Rails 3* book which I was reading on the subway ride to NYU which is where I was going to be spending the day. (My fiance works at NYU.) I read a couple chapters then started playing an episode of [*Ruby Rogues*](http://rubyrogues.com/) and switched back to deploying on Heroku again. That's when I became a victim of quick success. I resolved the last issue I was having yesterday pretty quickly and that got me excited thinking I just might be close to it working. (Not really.) And I kept telling myself, "But maybe this is the last error message before it works!".

I discovered (unfortunately not soon enough) that Heroku seems to run through the Rails app migrations sequentially one by one as it tries to build the database in PostgreSQL. Not sure why this is the way it does it but it just does. There has to be a better way. What was causing me problems was that every time Heroku came across a migration that did something that PostgreSQL did not like, it would puke some cryptic error about some DB incompatibility that most likely did not actually exist in my database any more. It existed in that particular migration it was trying to execute at the time but not in the current schema. Heroku was making me pay for offenses my db commited in its youth. So eventually I figured out that if I deleted the offending migration file and re-ran the migration, Heroku would get further before finding the next migration it didn't care for. Eventually I got it to finish the migration and Walla! the app came online.

Had lunch and afterwards joined my girlfriend in visiting a restaurant we're considering for our post-wedding dinner. Not happening til August 2014 but you can never start planning too soon.

After getting back, I decided to try to populate the production database with the data I had in my development database so I had something to work with. Shouldn't be too hard. All it should take is "heroku db:push", right? I entered the command, hit enter, and then a few seconds later I learned that Heroku wasn't done with me yet. "Time zone displacement out of range." Just rolls off the tongue doesn't it? Whatever was going on it caused the push to fail and the app to crash to boot. So I hit Google and Stack Overflow and tried to figure out what in the world this error might mean.

Long story short, I came across a proposed solution which I found hard to believe. You're gonna love this. The proposed solution was to switch to Ruby 1.9.2, reinstall the necessary gems, conduct the push, and then switch back to Ruby 1.9.3. Seriously? With great skepticism I tried it and wouldn't you know it, it worked. Apparently there's something about the Heroku db that is incompatible with Ruby 1.9.3. So the only way to get the data push to work is to use 1.9.2. Wow. But everything worked after that.

I ended the day looking into Sinatra. I installed the gem and created and ran my first, basic-as-it-gets Sinatra app. Looks pretty interesting. Can't wait to learn more.

"*Our greatest glory is not in never failing, but in rising up every time we fail*" - Ralph Waldo Emerson