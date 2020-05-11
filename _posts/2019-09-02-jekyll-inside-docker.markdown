---
title: "Jekyll Inside Docker"
date: 2019-09-02
---

To run Jekyll inside a docker container use the next scripts:

OSX

{% highlight bash %}
#!/bin/bash

# I usually create my local projects in /var/www/..., 
# but osx requires us to specify the real system path to link volumes.
# So, we can add /private prefix to the params in order to be able 
# run commands directly from /var/www

export JEKYLL_VERSION=3.6
docker run --rm \
    --volume="/private$PWD:/srv/jekyll" \
    --volume="/private$PWD/vendor/bundle:/usr/local/bundle" \
    -it jekyll/jekyll:$JEKYLL_VERSION jekyll "$@"
{% endhighlight %} 

Linux

{% highlight bash %}
#!/bin/bash

export JEKYLL_VERSION=3.6
docker run --rm \
    --volume="$PWD:/srv/jekyll" \
    --volume="$PWD/vendor/bundle:/usr/local/bundle" \
    -it jekyll/jekyll:$JEKYLL_VERSION jekyll "$@"
{% endhighlight %} 
