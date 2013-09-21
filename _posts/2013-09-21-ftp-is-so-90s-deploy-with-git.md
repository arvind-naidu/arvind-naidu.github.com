---
layout: post
title: "FTP Is So 90's. Deploy With Git."
---

First, create a directory on your server and initialize an empty git repository. I like to serve my websites from `~/www/`, so that's what I'll do in this example.

{% highlight javascript %}
mkdir ~/www/example.com && cd ~/www/example.com
git init
{% endhighlight %}

Next, let's set up your server's git repo to nicely handle deployment via git push.

{% highlight javascript %}
git config core.worktree ~/www/example.com
git config receive.denycurrentbranch ignore
{% endhighlight %}

Finally, we'll set up a post-receive hook for git to check out the master branch so your web server can serve files from that branch. (Remember, ^D is Control+D, or whatever your shell's [EOT character][EOT] is.

{% highlight javascript %}
cat > .git/hooks/post-receive
#!/bin/sh
git checkout -f
^D
chmod +x .git/hooks/post-receive
{% endhighlight %}

Keep in mind that you can add whatever you like to the post-receive hook if you have a build process. For example, one of my sinatra projects uses the following post-receive hook:

{% highlight javascript %}
#!/bin/sh
git checkout -f
bundle install
touch ~/www/example.com/tmp/restart.txt
{% endhighlight %}

Back on your local machine, let's get your git repo ready for deployment.

{% highlight javascript %}
cd ~/www-dev/example.com
git remote add origin \
ssh://user@example.com/home/user/www/example.com
{% endhighlight %}

For the first push to your server, run the following command.

{% highlight javascript %}
git push origin master
{% endhighlight %}

Now, whenever you want to deploy changes you've made locally, simply run the following command!

{% highlight javascript %}
git push
{% endhighlight %}

[EOT]: https://en.wikipedia.org/wiki/End-of-transmission_character "End-of-Transmission Character"