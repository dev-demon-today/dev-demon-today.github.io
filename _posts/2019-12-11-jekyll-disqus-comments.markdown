---
title: "Jekyll Disqus Comments"
date: 2019-12-10
---

Adding comments takes a few minutes.  

First, add this snippet

{% highlight js %}
<script src="{{ "/assets/js/disqusLoader.js" | relative_url }}" /></script>
<div id="disqus_thread"><h3>Discussion and feedback</h3></div>
<div class="disqus"></div>
<script>
    disqusLoader('.disqus', {
        scriptUrl: 'https://{% raw %}{{ site.disqus }}{% endraw %}.disqus.com/embed.js'
    });
</script>
{% endhighlight %}

Then we have to update 'post' template

{% highlight html %}

<div class="post">
  ...

  {{ content }}
</div>

{% raw %}
{% if page.comments %}
  {% include disqus_comments.html %}
{% endif %}
{% endraw %} 

...

{% endhighlight %}

And a little more update the settings

{% highlight yaml %}
# Default values
defaults:
  -
    scope:
      path: ""
      type: "posts"
    values:
      comments: true
      layout: "post"
{% endhighlight %}