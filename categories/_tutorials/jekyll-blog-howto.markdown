---
layout: post
title:  "Setting up a Jekyll Blog on Github Pages"
---

I have experience working with wordpress.com in terms of a blogging site, but I have a love/hate relationship with wordpress. I think it does help streamline a lot of the process if you just want a simple interface for publishing posts. But the moment you want to get more involved, the interface isn't super fantastic (in my opinion), so I decided to explore my options. I didn't want to build a site from scratch because I'm not too keen on web development so I wanted something that could work fairly easily right out of the box. A friend had recommended [Jekyll](https://github.com/jekyll/jekyll) and I personally really liked that it could integrate with Github pages. So I figured I'd try it out.

In case anyone else wants to try setting it up, here are some quick notes from the process I had to go through.
+ I mostly followed [these instructions](https://medium.com/20percentwork/creating-your-blog-for-free-using-jekyll-github-pages-dba37272730a), but there were a couple of gotchas I had to be mindful of:
+ In order to make sure the pages rendered properly I had to update my \_config.yml.
{% highlight yml %}
baseurl: "/blog" # the subpath of your site, e.g. /blog to match my repository name
url: "https://loganesian411.github.io" # the github pages url.
{% endhighlight %}
+ Lastly I updated my Gemfile because the comments in it told me too. But, unclear if this was necessary. The [gemfile](https://github.com/loganesian411/blog/blob/gh-pages/Gemfile#L13) provides instructions on what changes you need to make.

I'll be playing around with the site structure and using collections and pages in a way to help organize my thoughts coherently. Feel free to check out the [source](https://github.com/loganesian411/blog) directly.