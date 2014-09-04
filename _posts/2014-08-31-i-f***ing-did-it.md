---
layout:     post
title:      I f***ing did it
date:       2014-08-31 13:40:00
summary:    I end up with a blog after being challenged to have my web site finally up and running in two weeks
categories: blog
---

## Go fucking do it?

I have been talking about having my web site/blog it's been months, may be years, and now here it is!

I think the last drop in my procrastination bucket was when I accepted [@mauehara](https://twitter.com/mauehara)'s challenge on [gofuckingdoit.com](http://gofuckingdoit.com), meaning that I would have to pay cash $$ if I didn't have my website (with an [*about me*](http://felipe.sabino.me/about/) page) up and running within 2 weeks and well, [it worked!](https://gofuckingdoit.com/result/9db76259bb442fd0/)

Geeky as I am, I decided to share some technicalities about why I chose [Jekyll](jekyllrb.com) and end up running this page for free on [Github](https://github.com).

## Jekyll and Github

I am so surprised to see how technically simple it was have this blog up and running, but how hard it was to fill it up with (at least some) content. 

After some basic research trying to find the easiest\*, fastest and cheapest way possible to have a blog system, I end up sticking with the [Jekyll](jekyllrb.com) + [Github](https://github.com) solution. If you thinking about having your own blog, here are some thoughts on why I chose Jekyll and Github:

### Static content only

Yap, you read it, no server code, no databases, HTML only, totally static.

One point is that I have to deal with servers, scalability, databases, performance, cache, etc etc etc every single day and one thing I really wanted was to avoid this kind of headache. Not only that, HTML files you can host anywhere and you don't even need anything special about the server, I could put these HTML files in my dropbox\*\* folder if I wanted and everything would still work... it would be a bit slow, I know, but it would work and be *good enough*.

### Git/Github based

Jekyll is the engine that runs [Github Pages](https://pages.github.com) whih makes it [very simple to have you blog running on github](https://help.github.com/articles/using-jekyll-with-pages), with minimal setup possible. If the [github tutorial](https://help.github.com/articles/using-jekyll-with-pages) is not enought, [Matt West has a very detailed blog post explaining how to set up github pages and jekyll](http://blog.teamtreehouse.com/using-github-pages-to-host-your-website), also including details about the domain/subdomain setup that you would have to dig through Github's documentation.

Not only that, it makes easy to collaborate, If you find a bug or something that is not up-to-date, just go [the repository](https://github.com/felipesabino/felipesabino.github.io) and create an issue, or fix it and send me a pull request.

Pull requests are prettu handy, and it is something that I really wanted since the beggining. I got frustrated several times in the past about not being able to help [fix the internet](https://xkcd.com/386/), like one time the [objc.io #6](http://www.objc.io/issue-6/travis-ci.html) blog and was [asked to write an email with the issues I found](https://twitter.com/MattesGroeger/statuses/423221404369055744), nah..


### Markdown out of the box

Since I met [Haml](http://haml.info/) (back on the days), I just could never get used again to the plain old way of writting HTML tags, they seem so confusing and it is so easy to forget to close one and have a bad formatted document, so whenever I have the opportunity, I choose not to use it, opting for alternatives, like [Jade](http://jade-lang.com/) for Node.js based systems, for example.

Besides that, this is a blog, so it is supposed to be text oriented and I don't want to keep worrying about opening paragraph and image tags, I just want to focus on the content, which is something [markdown](http://daringfireball.net/projects/markdown/) is pretty good at and Jekyyl has as default.


## Alternatives

I also considered some other blog platforms before sticking to this one that might be suitable for you.

### Ghost

When [Ghost](https://ghost.org/) first [launched to the public](http://blog.ghost.org/public-launch/) almost an year ago I though it was an awesome idea, simple, no comments and open source.

The only downside for using Ghost was having to host it somewhere and (as I explained here already) this wasn't something I was willing to do, also I didn't want to [pay for the hosted solution](https://ghost.org/pricing/) as well, so I kept ghost as I backup in case I didn't have any other good options

### Medium

[Medium](https://medium.com/) was also an alternative but the problem is that I wanted to have a page of my own, my custom content, being able to add more stuff in the future (not that I would do it, but I want the option at least) and also be able to change style freely, so there you go, Medium was also not an option.

---

\* I know that easiest might not be a suitable term for everybody, my mom for example would surely find it impossible to do, or even start doing, but any developer should be able to do it just by reading github docs :p

\*\* Yes, I am aware of all the [crazy debate going on in the internet since Condoleezza Rice joined Dropbox's Board of Directors](http://www.drop-dropbox.com/), but you know what I meant, right?
