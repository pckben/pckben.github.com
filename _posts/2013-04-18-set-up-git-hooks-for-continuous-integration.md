---
layout: post
title: Set up git hooks for continuous integration
---

Create a git bare repo, a post-receive git hook and make it executable:

{% highlight bash %}
$ cd /path/to/deploy/repo.git
$ touch hooks/post-receive
$ chmod +x hooks/post-receive
$ vim hooks/post-receive
{% endhighlight %}

Insert the following code, but modify it to your taste, for example: add a line
for automatically execute tests, or syncing static website with an Amazon S3
bucket.

{% highlight bash %}
#!/bin/bash
#CONFIG
LIVE="/path/to/local/live/repo"
 
read oldrev newrev refname
if [ $refname = "refs/heads/master" ]; then
  echo "************* DEPLOYING TO LIVE SITE ******************"
  unset GIT_DIR
  cd $LIVE
  git pull origin master
  # do some other stuff here...
  echo "********************* DONE ****************************"
fi
{% endhighlight %}

Next, clone this bare repo into a local live repo

{% highlight bash %}
$ mkdir -p /path/to/local/live/repo
$ cd /path/to/local/live/repo
$ git clone /path/to/deploy/repo.git .
{% endhighlight %}

Now, go back to your working repo, add the deploy remote, then push to it to
deploy:

{% highlight bash %}
$ cd /path/to/working/repo
$ git remote add deploy /path/to/deploy/repo.git
$ git push -u deploy master
{% endhighlight %}

