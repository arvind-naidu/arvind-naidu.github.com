---
layout: post
title: "Share Localhost With Anyone"
---

Ever wanted to quickly share your localhost server with someone else, without going through the hassle of deploying it somewhere?

You’ll be happy to know that there’s a really simple way to do this. Firstly, install the localtunnel gem:

{% highlight javascript %}
$ gem install localtunnel
{% endhighlight %}

Next run your localhost server, for example in Rails, using the default WEBrick server:

{% highlight javascript %}
$ rails server
{% endhighlight %}

Or in Python:

{% highlight javascript %}
$ python - m SimpleHTTPServer 8000
{% endhighlight %}

The first time you run localtunnel, you’ll need to use one of your public SSH keys:

{% highlight javascript %}
$ localtunnel -k ~/.ssh/id_rsa.pub 8000
{% endhighlight %}

You’ll see something like this in your terminal:

➜  project_name git:(develop) localtunnel 8000
   This localtunnel service is brought to you by Twilio.
   Port 8000 is now publicly accessible from http://xxxx.localtunnel.com ...

Now just share `http://xxxx.localtunnel.com` with whoever that needs to see your work.

Subsequently you can just use localtunnel <port> to generate a public URL:

{% highlight javascript %}
$ localtunnel 8000
{% endhighlight %}

And that’s it. Installation and setup takes less than 5 minutes, and it works beautifully.