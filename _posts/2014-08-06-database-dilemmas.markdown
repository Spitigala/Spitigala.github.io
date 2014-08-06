---
layout: post
title:  "Database Deilemmas: A refelction on my final project at Dev Bootcamp"
date:   2014-08-06
categories: dbc devbootcamp coding
---


Designing database schemas can tricky, and as a relatively new developer, I’m bound to run in to my fair share of troubles with it. But the last thing I need is a schema design flaw 3 days before final presentations at Dev Bootcamp.

Since the universe works in mysterious ways to teach us life lessons, that’s exactly what happened to my team. Our final project was to build [smartSOS][smartsos], a platform that connects non-profits and donors. The basic idea is that non-profits can create a listing of items they need, and donors can respond accordingly by dropping off items they already have or buy them through Amazon and ship the items directly to the organization. You can checkout the code base [here][sourcecode].

Our first task was to figure out all the moving pieces of our application, and then translate that in to a schema design. What data do we need to store? How will this data interact with each other? What actions will our end users need to take in our app? These questions would drive the design for the foundation of our app, which would in turn drive the rest of our development process. 

After much deliberation we came up with the following:

- The app will have 2 types of users: Organizations and Donors.
- Each organization can create a campaign. 
- A campaign would consist of many requests.
- Each request consists of one item and a quantity for that item.
- A donor can give items to a campaign by making a pledge.

So what did our database design looks like?

![Imgur](http://i.imgur.com/gdV3SvM.png)


I know what you’re thinking. WTF is this mess?? 

Out here in these parts of town, we call it spaghetti.

We initially failed to see the bigger problem, although we felt something was off as our controllers were being built. We had to traverse lengthy paths to get to our data, but were unable to pinpoint the exact problem. The team was too deep in to the code to think of making any fundamental changes. In fact, we were already excited about adding new features.

Three days in to the project, we were called in for a consultation with our instructors [Steven][steventwitter] and [Nikola][nikolatwitter]. Their feedback was not what we wanted to hear. They expressed deep concern about our database design and recommended that we rethink our approach. But at that point it seemed as if we were too far in to the development process, and we still had a lot of work left to do. In our minds, a database redesign seemed too daunting, and as team lead I decided against it due to time constraints. I had never managed a technical project before. I didn’t know about the technical debt our mistake would bring, or the cost-benefit of doing a redesign. All I could think about was having a cool product to deliver on demo day to impress employers and the DBC community. I respected Steven’s input, but in the end decided to continue with our current iteration, which would turn out to be one of my biggest mistakes as a developer and a leader.

The following day, we were called in for a second meeting. 
This time around, our instructors’ attitude towards us had taken on a more serious tone. Basically, Steven tore us all apart. He said that it looked like we had “put the engine in backwards” and that none of it made sense to him. He suggested that rather than going back to fix what’s broken, we should rebuild the app from scratch, and that he knows we can get it done in time for demo day. This time he had my attention, and his confidence won me over.
When a programming veteran tells you that you screwed up, that you should change something, that he believes you can deliver on time, and does so with a straight face, you can bet anything that he means every word coming out of his mouth. So with just 3 days left to rebuild our app, we walked over to our terminal and hit RAILS NEW. 

It was scary. But in a weird way, it was exciting. My team was up for the challenge.

Here is the redesigned schema. 

![Imgur](http://i.imgur.com/0qm7A0r.png)

*Clean. Concise.*

It truly made a difference in our development process. Where as before we had to traverse lengthy paths to get to our data, our new design gave us paths that were more direct. Passing data around and writing tests became much easier too. 

We also shortened and decreased our routes by changing the nested routes structure. Here are our routes in version 1:

![Imgur](http://i.imgur.com/sjtHz3A.png)

And here they are in version 2:

![Imgur](http://i.imgur.com/JufU80L.png)

What’s more? In just one day, we were able to catch up to the exact point we had been at before we decided to go for the redesign. That’s 4 days of work packed in to a single day, and worth every effort by our awesome team.
So what lessons did I learn?

**Get feedback early and often.** We failed to run our database design through our instructors because we believed we had it right he whole time. Had we taken the time to consult them earlier in the process, we would have avoided our costly mistake.

**Listen to what others have to say, and give reasonable consideration to their feedback.** I’m not saying blindly follow someone’s advice because they’re more experienced. But rather, take the time to understand the logic behind their reasoning no matter how absurd it may sound at first. It certainly sounded crazy when our instructors initially asked us to change our approach. 

**Don’t be afraid to throw out code.** It’s easy to become attached to your code. After all, you worked so hard on it. But like in any relationship, you have to learn when to let go. Now go make a rom com out of that!

**Your final project is not about how cool your idea is.** It’s about your Engineering skills and how well you manage complexity. It’s about how you work as a team and perform under pressure of time constraints. It’s perfectly ok if your app isn’t full of every feature you wanted. It’s an MVP. Focus on making a few features work extremely well. But most importantly, make sure that you’re learning and improving your skills until the very end. It’s not a competition, even though it may feel like one at times. The real winner is the one who learns the most during the process.

Spring peepers out. *Peep peep!*


[smartsos]: http://smartsos.herokuapp.com
[sourcecode]: https://github.com/Spitigala/smartSOS-2.0
[steventwitter]: https://twitter.com/sgharms
[nikolatwitter]: https://twitter.com/JaNisamTesla
