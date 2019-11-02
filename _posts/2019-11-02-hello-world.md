---
layout: post
title: "Site Launched"
date: 2019-11-01
---
{% include mathjax.html %}

I'm playing around with putting a github.io website together. I consider myself a complete beginner in web/html/css/etc., so I had no idea what I was getting myself into when I started this project this morning. I thought it'd be easy with github.io, since they kind of have everything set up for you already, but I actually spent a good chunk of time chasing down blogs and tutorials. 

So here's a rough run down of how I spent my morning today. 

The first thing I did was I went to the [GitHub Pages](https://pages.github.com/) site and followed all of their instructions to set up a GitHub repo. I wanted to start with a theme, because I know that I have a pretty limited sense of design, so here I prefer to "stand on the shoulders of giants," at least for now. So I again followed GitHub's instructions [here](https://help.github.com/en/github/working-with-github-pages/adding-a-theme-to-your-github-pages-site-with-the-theme-chooser) to add a theme (I chose the [Tactile](https://github.com/pages-themes/tactile)
 theme to start with). This created a `_config.yml` file in my repo with a pointer to the correct theme (don't forget to `git pull`).

This is when I realized I had no idea what to do next to create some pages for my new site. Thankfully, this tutorial by [Jonathan McGlone](http://jmcglone.com/guides/github-pages/) gave me a really nice starting point.

After following that tutorial, I wanted to play around with some stuff even more. At this point, I knew I needed to setup a local environment to avoid without constantly pushing my mistakes to my live page. 

GitHub Pages supports [Jekyll](https://jekyllrb.com/), but I didn't have it yet locally. So first, I had to install some libraries to get everything to run on ubuntu (my current local operating system). In the end, I wanna say this is everything I installed (but I haven't tried it again in a fresh environment yet to confirm): 

{% highlight bash %}
{% raw %}
sudo apt-get install zlib1g-dev
sudo apt install ruby-all-dev
sudo gem install rubygems-update 
sudo update_rubygems
sudo gem install bundler jekyll
sudo gem install kramdown
bundler update github-pages
{% endraw %}
{% endhighlight %} 

Now I could view my own github.io page locally, meaning I could prototype more quickly. To run it locally, I had to execute this command, and simply point my browser to `http://127.0.0.1:4000`:

{% highlight bash %}
{% raw %}
bundle exec jekyll serve
{% endraw %}
{% endhighlight %}

Next, in order to be able to see the GitHub Pages themes locally, I had to create a `Gemfile` in my repo's main project folder and add these lines to it: 

{% highlight ruby %}
{% raw %}
source "https://rubygems.org"
gem "github-pages", group: :jekyll_plugins
{% endraw %}
{% endhighlight %}

Then I ran:

{% highlight bash %}
{% raw %}
bundle install
{% endraw %}
{% endhighlight %}

This got the themes installed, but in order to update the HTML/CSS of that theme with my own half-baked design ideas, I had to followed helpful instructions on the [Tactile](https://github.com/pages-themes/tactile) GitHub repo page.

Next, I knew that I would want to use math formulas in my blog posts, so I used [this](http://csega.github.io/mypost/2017/03/28/how-to-set-up-mathjax-on-jekyll-and-github-properly.html) tutorial on setting up $\LaTeX$ formulas. The tutorial shows how to create an importable bit of code that you can include in other pages to get `mathjax` to work. 

Unfortunately, the tutorial failed to mention how to actually import that bit of code. Being new to Jekyll, it took me a while to figure that out. Anyways, this is the line you need to add to every file you want to use formulas in:

{% highlight liquid %}
{% raw %}
{% include head.html %}
{% endraw %}
{% endhighlight %}

By the way, to show all of the code blocks above, I followed [this](https://tosbourn.com/liquid-raw-syntax/) guide about jekyll's `liquid` syntax, which tells you how to `highlight` code and how to escape code with the `raw` keyword. 
