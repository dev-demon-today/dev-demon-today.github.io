---
title: "Bash Aliases"
date: 2019-02-09
except: When you are young and hot, you think that everything is still ahead and that your time will never end, and life is something immeasurably large and boundless. But over time, you realize that spending your life repeating the same actions is a way of suckers. 
---

When you are young and hot, you think that everything is still ahead and that your time will never end,
and life is something immeasurably large and boundless.
But over time, you realize that spending your life repeating the same actions is a way of suckers.

<!--more-->

True Zen-masters never type long commands into a terminal twice.
They use the secret ninja technique to quickly backup, deploy or jump to a server in no time.
And as you might have guessed, we are talking about bash aliases.

![{{ page.title }}]({% link /assets/images/03-bash-aliases/03-bash-aliases.jpg %})

The best place for aliases is the ```~/.bash_aliases``` file, it will be connected every time a bash session starts.
it is absent by default, so we have to create it first:

{% highlight bash %}
nano ~/.bash_aliases
{% endhighlight %} 

Now we can add an alias, for example like this one:

{% highlight bash %}
alias mlog='tail -f /var/log/mysql/*'
{% endhighlight %} 

After changin the file we have to refresh bash session to apply the settings, like so:

{% highlight bash %}
. ~/.bash_aliases
{% endhighlight %} 

This alias should call ```tail -f /var/log/mysql/*``` when you type ```mlog```. 
Very helpful to access to db logs quickly.

Sometime we would want to have an ability to enable or disable query logging in mysql:

{% highlight bash %}
alias mquery_log_enable='mysql -e "SET global general_log = 1;"'
alias mquery_log_disable='mysql -e "SET global general_log = 0;"'
{% endhighlight %} 

Or take a look at webserver logs:

{% highlight bash %}
# nginx logs
alias nlog='tail -f /var/log/nginx/error.log /var/log/nginx/access.log'
{% endhighlight %} 

{% highlight bash %}
# apache logs
alias alog='tail -f /var/log/apache2/access.log /var/log/apache2/error.log'
{% endhighlight %} 

Restart web server:

{% highlight bash %}
# nginx restart
alias nrestart='sudo service nginx restart'
 
# apache restart
alias arestart='sudo service apache2 restart'
{% endhighlight %} 

Open webserver config file even if you cant remember your own name after the last night party: 

{% highlight bash %}
# edit nginx config
alias nconfig='sudo subl /etc/nginx'
{% endhighlight %} 

{% highlight bash %}
# edit apache config
alias aconfig='sudo subl /etc/apache2'
{% endhighlight %} 

Edit /etc/hosts:

{% highlight bash %}
alias hosts='sudo subl /etc/hosts'
{% endhighlight %} 

When you work with a local repo you would want to ignore local file permissions: 

{% highlight bash %}
alias git-ignore-chmod='git config core.fileMode false; git config --global core.filemode false;'
{% endhighlight %} 

To connect to a remove server by ssh:

{% highlight bash %}
alias socks5='ssh -o "StrictHostKeyChecking no" -D 12345 -f -C -N ubuntu@proxy5.aws'
{% endhighlight %} 

Or, even my very strange case. Sometimes I want to restart all php-fpm versions I use on my machine:

{% highlight bash %}
alias php-restart='sudo service php5.6-fpm restart; sudo service php7.0-fpm restart; sudo service php7.1-fpm restart; sudo service php7.2-fpm restart;'
{% endhighlight %} 

Set default file permissions for the current dir and all sub dirrectories:

{% highlight bash %}
# chmod files to 644
alias chmod-files='sudo find ./ -type f -exec chmod 644 {} \;'

# chmod directories to 755
alias chmod-dirs='sudo find ./ -type d -exec chmod 755 {} \;'
{% endhighlight %} 

Run a docker container:

{% highlight bash %}
# run metasploit
alias metasploit='docker run --rm -it --net="host" -p 8080:443 -v ~/.msf4:/root/.msf4 -v /tmp/msf:/tmp/data remnux/metasploit'
{% endhighlight %} 

Copy your public key to clipboard:

{% highlight bash %}
alias get-public-key='xclip -sel clip < ~/.ssh/id_rsa.pub'
{% endhighlight %} 

Connect to ssh without typing ip or domain:

{% highlight bash %}
# Dev server
alias ssh_dev_server='ssh ubuntu@12.123.123.12'

# Stage server
alias ssh_stage_server='ssh ubuntu@34.345.34.345'
{% endhighlight %} 

Or just run a script:

{% highlight bash %}
# Deploy
alias deploy='~/scripts/deploy.sh'

# Backup
alias backup='~/scripts/backup.sh'
{% endhighlight %} 

That's it. Now you have this real ninja tool and the next time when you 
will copy-paste something from stackoverflow remember that by entering or copying the same commands each time, 
you just bring the heat death of the universe.