---
published: true
title: My Journey to Jekyll
excerpt_separator: <!--more-->
categories:
  - Web Design
  - Tutorials
tags:
  - jekyll
  - github
  - github-pages
  - markdown
---
![My Journey to Jekyll](https://jekyllrb.com/img/logo-2x.png)

About a week ago or so, I started searching around for a way for me to publicize thoughts, ideas, and cool things I encounter daily.  I had quite a few requirements for my new website:

* It should cost nothing.
* It should have a small footprint.
  * _Containerized, hosted for free, whatever..._
* It shouldn't rely on a database.

Three requirements... and no idea where to start.  Wordpress has failed me in the past, Joomla is out of the question, and CMS as a whole just isn't as appealing to me anymore.  Plus, mosted of the hosted sites are insecure themselves and are typically breached.

I did play around with the idea of [GitHub Pages](https://pages.github.com/) in the past and made a static content site at [https://git.joeco.de](https://git.joeco.de), so I figured it was about time to _actually_ dive deep into Jekyll this time.

<!--more-->

I immediately went to the official [Jekyll website](https://jekyllrb.com) and was happy to see a nice lower-third banner for "Free Hosting on GitHub Pages."  Perfect!

I eventually landed myself on the [Jekyll-Now](https://github.com/barryclark/jekyll-now) GitHub repo for a super easy theme that can be forked.

1. Fork the [Jekyll-Now](https://github.com/barryclark/jekyll-now) GitHub repo.
2. Click `Settings` on your newly created GitHub repo and scroll to the **GitHub Pages** section.
3. Under **Source** select the dropdown box `None` and select `Master Branch`.
4. Click `Save`.
5. Navigate to **https://username.github.io/jekyll-now** where `username` is your GitHub username.
6. You should see something similar to this: [https://git.joeco.de/infamousjoeg.github.io-jekyll-now/](https://git.joeco.de/infamousjoeg.github.io-jekyll-now/)

Now, to create posts, just add markdown files to `_posts` in the format `YYYY-MM-DD-Your-Title.md` or, you can be like me, and head over to [Prose.io](https://prose.io) and use that to take a lot of the pain away.

Here's an example of my first test post: [_posts/2017-10-11-Hey-you-shouldn't-be-here!.md](https://raw.githubusercontent.com/infamousjoeg/infamousjoeg.github.io-jekyll-now/gh-pages/_posts/2017-10-11-Hey-you-shouldn't-be-here!.md)

Notice the content wrapped in `---`?  That's called **Front Matter**.  That is the header of the post that dictates the styling and other metadata (which is exactly what Prose.io calls it instead of Front Matter).  My front matter in the example post is saying to use the `post` layout and set the title to `Hey, you shouldn't be here!`  Which we see on the rendered page at [https://git.joeco.de/infamousjoeg.github.io-jekyll-now/Hey-you-shouldn't-be-here!/](https://git.joeco.de/infamousjoeg.github.io-jekyll-now/Hey-you-shouldn't-be-here!/).

You can continue to dive deeper from there... and maybe we will in a future post.  However, that's it for now -- check back later for more!
