# Jekyll test

A test of hosting a proper Jekyl site on Github
inside the `docs` dir.

Doco should be live [here](https://tcab.github.io/jekylltest/)

I simply followed the [official tutorial](https://jekyllrb.com/docs/)

## Deployment to Github pages

This was tricky, since the urls were slightly off.

The solution was found here
https://byparker.com/blog/2014/clearing-up-confusion-around-baseurl/
viz.
Place the subdirectory name github pages will serve from (which is simply **the name of the github repository**) in  `_config.yml`:

```yaml
baseurl: "/jekylltest"
```

This forces the local server to serve on the same path as github does e.g. 
http://127.0.0.1:4000/jekylltest/

Then adjust all urls to prepend that 'baseurl' - here are lots of examples:

```html
{{ page.path | prepend:site.baseurl }}

<h2><a href="{{ post.url | prepend:site.baseurl }}">{{ post.title }}</a></h2>
<h2><a href="{{ author.url | prepend:site.baseurl }}">{{ author.name }}</a></h2>

<nav>
    {% for item in site.data.navigation  %}
        <a href="{{item.link | prepend:site.baseurl}}" 
           {% if page.url == item.link %} class="current"{% endif %}
        >
        {{item.name}}</a>
    {% endfor %}
</nav>

<ul>
  {% assign filtered_posts = site.posts | where: 'author', page.short_name %}
  {% for post in filtered_posts %}
    <li><a href="{{ post.url | prepend:site.baseurl}}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

```

etc.

### Fixing stylesheet paths

Had to innovate a slight trick. Define a variable in `_config.yml`:

```yaml
assets: "/assets/css/styles.css"
```

then in 
`docs/_layouts/default.html`
refer to that variable and do the same prepend trick:
```
 <link rel="stylesheet" href="{{ site.assets | prepend:site.baseurl }}">
```

## Install and Run

`bundle install` or `bundle update` to install stuff from the Gemfile

Run locally at http://127.0.0.1:4000/jekylltest/ with `bundle exec jekyll serve`.  This builds the `_sites` dir and serves from that on port 4000.  

Also see handy script in `bin` dir called `run`.

Push to Github to run remotely on Github Pages. 
Remember to change Github repository **settings** in that particular github project to
* enable Github Pages, and 
* to server from the `docs` dir (choose this from the dropdown).

Github will then build the `_sites` dir and serve from that, just like you do locally when you run jekyll.

