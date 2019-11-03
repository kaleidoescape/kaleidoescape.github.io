---
layout: post
title: "Site Launched"
date: 2019-11-02
---

I consider myself a complete beginner in web/html/css/etc., so I had no idea what I was getting myself into when I started putting this website together this morning. I thought it'd be easy with github.io, since they kind of have everything set up for you already, but I actually spent a good chunk of time chasing down tutorials. So here's a quick and dirty summary of how I finally got things more or less up and running.

The first thing I did was I went to the [GitHub Pages](https://pages.github.com/) site and followed all of their instructions to set up a GitHub repo. I also made sure to `git clone` my repo, so I could work on the website in my text editor instead of through the GitHub website. The blog it gets updated on live whenever I do a `git push` to master (although it takes a few minutes to update the website). 

I wanted to start with a pre-built theme for my website, because I know that I have a pretty limited sense of design, so I again followed GitHub's instructions [here](https://help.github.com/en/github/working-with-github-pages/adding-a-theme-to-your-github-pages-site-with-the-theme-chooser) to add a theme (I chose the [Tactile](https://github.com/pages-themes/tactile)
 theme to start with, but later changed to the [jekyll-now](https://github.com/barryclark/jekyll-now) theme). This created a `_config.yml` file in my repo with a pointer to the correct theme.

This is when I realized I had no idea what to do next to create some pages for my new site. Thankfully, this tutorial by [Jonathan McGlone](http://jmcglone.com/guides/github-pages/) gave me a really nice starting point.

After following that tutorial, I wanted to play around with some stuff even more. At this point, I knew I needed to setup a local environment to avoid constantly pushing my mistakes to my live page. 

GitHub Pages supports [Jekyll](https://jekyllrb.com/), but I didn't have it yet locally. So first, I had to install some libraries to get everything to run on Ubuntu  18.04 (my current local operating system). I `cd`ed into my git repo project directory, and ran a whole bunch of commands, trying to get things to work. In the end, I think this is everything I had to install: 

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

Now I could view my own github.io page locally, meaning I could prototype more quickly. To run it locally, I had to execute this command from within my git repo project directory, and simply point my browser to `http://127.0.0.1:4000`:

{% highlight bash %}
{% raw %}
bundle exec jekyll serve
{% endraw %}
{% endhighlight %}

When I ran it, I realized the the Tactile theme didn't show up. In order to be able to see the GitHub Pages themes locally, I had to create a `Gemfile` in my repo's main project folder and add these lines to it: 

{% highlight ruby %}
{% raw %}
source "https://rubygems.org"
gem "github-pages", group: :jekyll_plugins
{% endraw %}
{% endhighlight %}

Then I ran:

{% highlight bash %}
{% raw %}
bundle install --path vendor/bundle
{% endraw %}
{% endhighlight %}

This got the themes installed, but in order to update the HTML/CSS of that theme with my own half-baked design ideas, I followed the helpful instructions on the [Tactile](https://github.com/pages-themes/tactile) GitHub repo page.

Next, I knew that I would want to use math formulas in $\LaTeX$ in my blog posts. There's a number of [blog posts](http://www.gastonsanchez.com/visually-enforced/opinion/2014/02/16/Mathjax-with-jekyll/), [tutorials](http://csega.github.io/mypost/2017/03/28/how-to-set-up-mathjax-on-jekyll-and-github-properly.html), [SO questions](https://stackoverflow.com/questions/40440863/mathjax-dont-show-up-on-jekyll-github-pages-but-show-up-on-localhost) and [issues](https://github.com/github/pages-gem/issues/307) on how to deal with problems surrounding this, but it took me a while to piece together the whole picture for my use case. Long story short, I am now using `mathjax`. 

Here's what I had to do to set that up.

First of all, create a file in `_includes/mathjax.html` with the following content:

{% highlight html %}
{% raw %}
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    TeX: {
      equationNumbers: {
        autoNumber: "AMS"
      },
      extensions: ["color.js"]
    },
    tex2jax: {
      inlineMath: [ ['$','$'], ['\\(', '\\)'] ],
      displayMath: [ ['$$','$$'] ],
      processEscapes: true,
	  processEnvironments: true,
	  skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
    }
  });
</script>

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
{% endraw %}
{% endhighlight %}

This content tells `mathjax` how to process math environments (both inline and block style), includes the `color` extension for making colourful equations, and sources the `mathjax` JavaScript code from a secure CDN (from an `https` location, instead of `http`). This last part is important for the formulas to work not just locally but also on GitHub Pages.

Next, we need to add this line in the `<head>...</head>` section of the `_layouts/default.html` file:

{% highlight liquid %}
{% raw %}
{% include mathjax_support.html %}
{% endraw %}
{% endhighlight %}

This will ensure that the mathjax code gets included in every page that uses the default layout. Now I can make equations, e.g using this code:

{% highlight liquid %}
{% raw %}

$$
\definecolor{blue01}{RGB}{38,139,210}
$$

Inline equation: $a+b=c$

$$ { \color{blue01} E } = mc^2$$
{% endraw %}
{% endhighlight %}

Produces this text:

$$
\definecolor{blue01}{RGB}{38,139,210}
$$

> Inline equation: $a+b=c$
>
> $${ \color{blue01} E } = mc^2$$

One thing I haven't figured out yet is how to change the size or colour of the equations in the equation environment. I guess I will have to leave that off to another day.


By the way, to show all of the code blocks above, I followed [this](https://tosbourn.com/liquid-raw-syntax/) guide about jekyll's `liquid` syntax, which tells you how to highlight code and how to escape code with the `raw` keyword. 


There's more formatting to be done on the blog, I still have to learn how `mathjax` is different from $\LaTeX$, and how to do a bunch of stuff, but at least the site looks sort of not the worst now. Yay! XD  
